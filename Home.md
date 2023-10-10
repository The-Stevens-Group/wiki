Welcome to the SG User Wiki. This a great place to start for accessing computing machines.

## SG Clusters at Imperial

The SG Cluster comprises a range of high-performance and cost-effective server solutions, 
encompassing both conventional CPU-based PC/server machines. Detailed information about the 
software and hardware components can be found on the dedicated [[Software]] and [[Hardware]] pages.

These machines are equipped with fast local storage capabilities. Store files on OneDrive, however, requires utilizing web browsers such as Firefox or Chrome.

The SG Cluster is exclusively designed for hosting web applications and executing resource-intensive 
applications (e.g. ML training jobs), or applications demanding dedicated hardware resources unavailable 
on conventional computing systems (e.g. GPUs, multiple CPUs).

## Connecting

### Linux Servers

You should have access to some of our servers from within the College network. If you are familiar with the Linux command line, you can simply execute the following commands using the Terminal or Windows PowerShell.

```
ssh sggpu1.doc.ic.ac.uk
```

However, we recommend utilizing X2Go because it creates a virtual local display on the remote server, enabling your software to run remotely. This approach ensures reliability, as it allows all operations to be performed locally on the build machine.
