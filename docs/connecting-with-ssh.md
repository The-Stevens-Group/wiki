# Connecting to a Linux server with SSH

SSH gives you a terminal on a server without a remote desktop. It is lighter and faster than x2go, works well on slow connections, and is how VS Code and coding agents connect. If you need graphical applications, use [x2go](connecting-with-x2go.md) instead.

## 1. Before you start

* You need a Linux account. See [Request a Linux Account](connecting-with-x2go.md#1-request-a-linux-account).
* Connect to the MSD VPN whenever you are outside the MSD network. See [Connect to MSD Network Using MSD VPN](connecting-with-x2go.md#2-connect-to-msd-network-using-msd-vpn).
* You need an SSH client. It is already installed on macOS and Linux (use `Terminal`) and on Windows 10 and 11 (use `PowerShell` or `Terminal`).

## 2. Connect

Run this on your own computer, using a hostname from the [list of machines](hardware.md):

```bash
ssh <your-username>@<hostname>
```

For example, `ssh jsmith@dragonair.dpag.ox.ac.uk`.

* The first time you connect to a machine, you are asked whether to trust it. Type `yes`.
* Enter your Linux account password. Nothing appears on screen while you type it.
* On your first login, [change your password](changing-your-password.md) by running `passwd`.

Type `exit` to disconnect.

## 3. Log in without typing your password

Create an SSH key once, then copy it to each machine you use. Run these on your own computer.

```bash
ssh-keygen -t ed25519        # only if you do not already have a key; press Enter to accept the defaults
ssh-copy-id <your-username>@<hostname>
```

On Windows, use this in PowerShell instead of `ssh-copy-id`:

```powershell
type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh <your-username>@<hostname> "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

## 4. Add a shortcut

Add an entry to `~/.ssh/config` on your own computer for each machine you use. On Windows, this file is `C:\Users\<you>\.ssh\config`.

```
Host dragonair
    HostName dragonair.dpag.ox.ac.uk
    User <your-username>
```

You can then connect with `ssh dragonair`, and VS Code lists `dragonair` as a host.

## 5. Use VS Code

1. Set up a key and a shortcut as above.
2. Install the **Remote - SSH** extension.
3. Run `Remote-SSH: Connect to Host...` from the command palette and choose your shortcut.

VS Code then edits files and opens terminals on the server.

## 6. Copy files

Run these on your own computer:

```bash
scp results.csv dragonair:~/project/                 # copy a file to the server
scp dragonair:~/project/figure.png .                  # copy a file from the server
rsync -av --progress data/ dragonair:/data/<your-username>/data/   # copy a folder, skipping files already copied
```

## 7. Keep work running after you disconnect

Anything started in a plain SSH session stops when the connection drops. Start a `tmux` session first, and your work keeps running:

```bash
tmux new -s work          # start a session
tmux attach -t work       # reconnect to it later
```

Press `Ctrl-b` then `d` to leave a session running in the background.

On Dragonair, GPU and heavy work should run as Slurm jobs instead, which keep running without `tmux`. See [Using Dragonair and Slurm](dragonair-and-slurm.md).
