## SG Clusters at Imperial

The SG Cluster comprises a few high-performance and low-cost server solutions, 
encompassing both conventional CPU-based PC/server and machines with GPUs. Detailed information about the 
hardware components can be found on the dedicated [[Hardware]] pages.

These machines are equipped with fast local storage capabilities. Storing files on OneDrive, however, requires utilizing web browsers such as Firefox or Chrome.

The SG Cluster is dedicated to hosting web applications and executing resource-intensive 
applications (e.g. ML training jobs), or applications demanding dedicated hardware resources unavailable 
on conventional computing systems (e.g. GPUs, multiple CPUs).

## Connecting

### Linux Servers

If you have contacted the administrator to open a user account, you should have access to some of our servers from within the College network. If you are familiar with the Linux command line, you can simply execute the following commands to access the machines using the Terminal or Windows PowerShell.

```
ssh sggpu1.dept.ic.ac.uk
```
### x2Go

However, we recommend utilizing X2Go because it creates a virtual local display on the remote server, enabling your software to run remotely. This approach ensures reliability, as it allows all operations to be performed locally on the build machine.

You need to first download X2Go client on your local machine:
https://wiki.x2go.org

The package is available on Windows, Linux and Mac.

After the installation, you have to create a local profile with the following steps:
1. Click `Session` -> `New session`.
2. Put the hostname or IP address of the remote server that you want to connect to, such as `sggpu1.dept.ic.ac.uk` or `172.22.42.169` as `Host`.
3. Put your userID as `Login`.
4. Select `MATE` as `Session type`.
5. Click `OK`.

You can connect to the remote machine by double-clicking the profile. It should prompt for your SG cluster password.

If you are connecting for the first time, it will prompt `The server is unknown. Do you trust the key?` Please press `Yes` to continue.

Note that this connection only works if you are in the College network, or [Unified Access](https://www.imperial.ac.uk/admin-services/ict/self-service/connect-communicate/remote-access/unified-access/) to the College 

## Change your password
If your account has just been created we advise that you change the default password. You can do so by following these instructions:

1. Right-click on the X2Go Desktop, and select `Open in Terminal`.
2. When the command line prompt shows up, type `passwd` and press Enter.
3. Enter your current password.
4. Enter the new user password.
5. Retype the new password a second time. You should then receive the message that the password has successfully been updated.

## Disconnecting
You can easily exit by clicking the `X` button located at the top right. Your ongoing sessions will be preserved for your next login through X2Go.

If you don't want to keep your current session, you can `log out` or `shut down` by clicking the top right gear button.
