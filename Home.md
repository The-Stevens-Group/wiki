Welcome to the SG User Wiki. This a great place to start for accessing computing machines.

## SG Clusters at Imperial

The SG Cluster comprises a range of high-performance and cost-effective server solutions, 
encompassing both conventional CPU-based PC/server machines. Detailed information about the 
software and hardware components can be found on the dedicated [[Hardware]] pages.

These machines are equipped with fast local storage capabilities. Store files on OneDrive, however, requires utilizing web browsers such as Firefox or Chrome.

The SG Cluster is exclusively designed for hosting web applications and executing resource-intensive 
applications (e.g. ML training jobs), or applications demanding dedicated hardware resources unavailable 
on conventional computing systems (e.g. GPUs, multiple CPUs).

## Connecting

### Linux Servers

You should have access to some of our servers from within the College network. If you are familiar with the Linux command line, you can simply execute the following commands using the Terminal or Windows PowerShell.

```
ssh sggpu1.dept.ic.ac.uk
```

However, we recommend utilizing X2Go because it creates a virtual local display on the remote server, enabling your software to run remotely. This approach ensures reliability, as it allows all operations to be performed locally on the build machine.

You need to first download X2Go client on your local machine:
https://wiki.x2go.org

The package is available on Windows, Linux and Mac.

After the installation, you have to create a local profile with the following steps:
1. Click `Session` -> `New session`.
2. Put the hostname or IP address of the remote server that you want to connect to, such as `sggpu1.dept.ic.ac.uk` or 172.22.42.169 as `Host`.
3. Put your userID as `Login`.
4. Select `MATE` as `Session type`.
5. Click `OK`.

Then you can connect to the remote machine by doubling the profile. It should prompt for your SG cluster password.

If you are connecting for the first time, it will prompt "The server is unknown. Do you trust the key?" Please press 'Yes'

Note that this connection only works if you are in the College network.
