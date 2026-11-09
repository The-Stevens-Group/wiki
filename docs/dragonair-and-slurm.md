# Using Dragonair and Slurm

Dragonair is the group's shared GPU workstation. You log in and edit freely, and GPU or heavy CPU work goes through the [Slurm](https://slurm.schedmd.com/) job queue, so everyone gets a fair share and can see what is running.

| | |
|---|---|
| **Hostname** | `dragonair.dpag.ox.ac.uk` (also `lin-mms009`) |
| **Available to jobs** | 56 CPU threads (28 cores), about 449 GB RAM, 2 × RTX Pro 6000 (96 GB each) |
| **Storage** | `/home/<you>` for code and environments, `/data/<you>` for datasets, checkpoints and logs |

## 1. Get access

1. Email the Stevens Group IT admin to request a Linux account, and include your MSD account name. See [Request a Linux Account](connecting-with-x2go.md#1-request-a-linux-account).
2. Ask them to add you to Slurm at the same time. You can log in without this, but you cannot submit jobs.
3. Connect to the [MSD VPN](https://www.medsci.ox.ac.uk/for-staff/resources/information-technology/document-and-file-storage/vpn) whenever you are working from outside the MSD network.

## 2. Connect

Pick one. Both give you the same files and the same queue.

### SSH and VS Code

Follow [Connecting with SSH](connecting-with-ssh.md) and use `dragonair.dpag.ox.ac.uk` as the host. Setting up a key and the `dragonair` shortcut there lets you run `ssh dragonair`, and choose `dragonair` in VS Code.

VS Code runs in your login session and does not use the queue. Start GPU work from the VS Code terminal as described below.

### Remote desktop (x2go)

Follow the [x2go guide](connecting-with-x2go.md) and use `dragonair.dpag.ox.ac.uk` as the host.

## 3. The one rule

**Anything that uses a GPU, or more than a few CPU cores, goes through Slurm.**

Editing, git, installing packages, small scripts and quick checks such as `nvidia-smi` are fine in your login session. Each user's login sessions share a limit of 8 CPUs and 48 GB of RAM, and processes are killed at 64 GB. Slurm jobs do not count towards this limit.

Slurm cannot see GPU work started outside it. If you run GPU work directly, Slurm may give the same GPU to someone else, and either job can then run out of GPU memory.

## 4. Run jobs

**Batch job**, which keeps running after you disconnect:

```bash
sbatch --gres=gpu:1 -c 8 --mem=64G -t 4:00:00 -J myjob --wrap "python train.py"
```

| Flag | Meaning | Default if omitted |
|---|---|---|
| `--gres=gpu:N` | Number of GPUs | No GPU |
| `-c N` | CPU threads | 1 core (2 threads) |
| `--mem=64G` | RAM. The job is killed if it goes over | 7 GB per CPU thread |
| `-t H:MM:SS` | Time limit. The job is stopped when it is reached | 4 hours, maximum 3 days |

A job always gets a whole GPU, even if it uses only part of the GPU's memory.

Your active Python environment carries over into the job. Output goes to `slurm-<jobid>.out` in the directory you submitted from.

**Batch script**, for anything you want to repeat:

```bash
#!/bin/bash
#SBATCH -J myjob
#SBATCH --gres=gpu:1
#SBATCH -c 8
#SBATCH --mem=64G
#SBATCH -t 4:00:00
#SBATCH -o /data/%u/slurm-logs/%x-%j.out
set -euo pipefail
source ~/myenv/bin/activate
python train.py "$@"
```

Run `mkdir -p /data/$USER/slurm-logs` once first, because the job fails if its log directory does not exist. Then submit with `sbatch train.sbatch`.

**Interactive shell with a GPU**, which also works in a VS Code terminal:

```bash
gpu-shell                      # 1 GPU, 8 CPUs, 64 GB, 4 hours
gpu-shell 2 16 128G 8:00:00    # GPUs, CPUs, memory, time
```

The shell holds its GPU until you type `exit`. It also ends if your connection drops, unless you started it inside `tmux`.

**Jupyter**, with `jupyterlab` installed in your active environment:

```bash
slurm-jupyter                  # 1 GPU, 8 CPUs, 64 GB, 8 hours
```

It prints a URL and the job id. Forward the port as described in the next section, open the URL, and run `scancel <jobid>` when you finish.

## 5. See what is running

**The job board** shows every user's running and queued jobs, GPU use, GPU processes running outside Slurm, and usage over the last 7 days. It only listens on the machine itself, so forward port 8080 first:

* **VS Code:** open the `Ports` panel and add port `8080`.
* **Terminal:** run `ssh -L 8080:127.0.0.1:8080 dragonair` on your own computer, and leave it running.

Then open <http://localhost:8080>. If port 8080 is already in use on your computer, use `-L 18080:127.0.0.1:8080` and open <http://localhost:18080> instead.

**From the command line:**

```bash
squeue                         # everyone's jobs
squeue -u $USER                # your jobs
scancel <jobid>                # cancel a job
sacct -X -S today              # your jobs from today, including finished ones
sshare -a                      # fair-share standings
scontrol show job <jobid>      # full details of one job
```

## 6. How fair use works

* **Priority:** fair share decides who goes next, so the less you have used recently, the sooner your queued jobs start. Past usage counts half as much after each week. Time waiting in the queue also raises priority, and smaller jobs get a slight boost.
* **Limits per user:** 10 running jobs and 200 queued jobs.
* **Running jobs are not interrupted:** priority only decides what starts next. Shorter jobs can also start sooner if they fit in a gap.
* **Isolation:** a job can only use the GPUs it was given, and it cannot use more memory than it requested.

## 7. Good habits

1. **Request what you need.** Realistic GPU, memory and time requests let more jobs run, and short jobs start sooner.
2. **Release GPUs when you stop.** Exit `gpu-shell` and cancel idle notebooks, because an idle session blocks a whole GPU from everyone else.
3. **Use one GPU unless your code needs two.** One job can otherwise hold both GPUs for days.
4. **Save checkpoints** in anything long, because jobs stop at their time limit, and 3 days is the maximum.
5. **Tell your agents to use Slurm** (see the next section).

## 8. Using agents (Claude Code, Codex, and others)

Agents use the same queue and the same limits as you. Unless told otherwise, they will usually run work directly, so add this to your project's `CLAUDE.md` or `AGENTS.md`:

```markdown
## Running jobs on dragonair
This is a shared machine. Run all GPU and heavy CPU work through Slurm, never directly.
- Submit: `sbatch --parsable --gres=gpu:1 -c 8 --mem=64G -t 4:00:00 -J <name> -o /data/$USER/slurm-logs/%x-%j.out --wrap "<command>"`. This prints the job id.
- Request only what the job needs, and set a realistic time limit.
- Check one job: `sacct -j <jobid> -X -n -o state`
- Queue as JSON: `squeue --json`. Machine-wide state: `curl -s localhost:8080/api/state`
- At most 10 of your jobs run at once. Extra jobs wait in the queue, so do not retry them.
- Only cancel your own jobs.
```

## 9. Troubleshooting

| What you see | What it means | What to do |
|---|---|---|
| `Invalid account or account/partition combination specified` | You have not been added to Slurm | Ask the IT admin to add you |
| `Requested node configuration is not available` | You asked for more GPUs or memory than dragonair has | Request at most 2 GPUs and 449 GB |
| `More processors requested than permitted` | You asked for more than 56 CPU threads | Lower `-c` |
| `Requested time limit is invalid` | You asked for more than 3 days | Lower `-t`, and resume from a checkpoint |
| Job is pending with reason `Resources` | The CPUs, memory or GPUs it needs are in use | Wait |
| Job is pending with reason `Priority` | Other queued jobs go first | Wait |
| Job is pending with reason `QOSMaxJobsPerUserLimit` | You already have 10 jobs running | Wait, or cancel one |
| Job state is `OUT_OF_MEMORY` | It went over `--mem` | Request more memory |
| Job state is `TIMEOUT` | It reached its `-t` limit | Request more time, or resume from a checkpoint |
| Job state is `FAILED` | Your command exited with an error | Read the job's output file |
| Your login session is slow, or a process was killed | It reached the login-session limits | Run the work through Slurm |
| CUDA out of memory, although your job has its own GPU | Something running outside Slurm may be using that GPU | Check the job board, and contact the user shown or the IT admin |
| GPU numbers differ between Slurm and `nvidia-smi` | Slurm's GPU 0 is the card `nvidia-smi` calls GPU 1, and the other way round | Nothing. Inside a job, its GPUs are always numbered from 0 |

Shared services such as Ollama, and containers started with `docker run`, run outside Slurm. The queue does not reserve resources for them or limit them.

## 10. For admins

Add a new user, after their Linux account exists:

```bash
sudo sacctmgr -i add user <username> account=stevens
sudo install -d -o <username> -g stevensgroup -m 700 /data/<username>
```

Other useful commands:

```bash
sudo sacctmgr modify qos normal set MaxJobsPerUser=10      # change the per-user running-job limit
sudo scontrol update nodename=lin-mms009 state=resume      # return the node to service if it shows as drained
systemctl status slurmctld slurmd slurmdbd slurm-portal    # check the services
```

Configuration is in `/etc/slurm/`, logs are in `/var/log/slurm/`, and the job board is in `/opt/slurm-portal/`. A copy of the quick reference is at `/data/local_libs/SLURM.md` on the machine.
