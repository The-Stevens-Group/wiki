All nodes run 64-bit operating systems:

| Node     | OS         | Remarks |
|----------|------------|-----------|
| sgcad1.dept.ic.ac.uk | Ubuntu 20.04  | Nginx |
| sggpu1.dept.ic.ac.uk  | Ubuntu 20.04 | CUDA 12.2 |

The following software is installed in `/opt` on sggpu1:

1. MATLAB 2020a
2. [Opening and Closing Surfaces](https://github.com/sgsellan/opening-and-closing-surfaces#opening-and-closing-surfaces)

## Global Software
### Opening and Closing Surfaces
1. Right-click on the X2Go Desktop, and select `Open in Terminal`.
2. When the command line prompt shows up, type or copy the following:
```
cd;
/opt/launch_oc.sh
```
Matlab 2020a should be launched with `opening-and-closing-surfaces` libraries available to use

### Matlab 2020a
1. Right-click on the X2Go Desktop, and select `Open in Terminal`.
2. When the command line prompt shows up, type or copy the following:
```
cd;
/opt/MATLAB/R2020a/bin/matlab
```
## Local Software
### OligoMiner and Nupack (Inga)
1. Right-click on the X2Go Desktop, and select `Open in Terminal`.
2. When the command line prompt shows up, type or copy the following to launch the software that you need:

#### OligoMiner
```
cd /home/ingavdb/OligoMiner/;
conda activate probeMining;
```
Visit https://github.com/beliveau-lab/OligoMiner and go to the section on **Running OligoMiner locally**

#### Nupack

To run Nupack 4.0.1.8 properly, you have to deactivate the conda environment so that you can use the default Python3 that comes with Ubuntu.

```
conda deactivate;
cd /home/ingavdb/workspace/;
source /home/ingavdb/venv_nupack/bin/activate;
jupyter lab
```

It should start Jupyter Notebook in Firefox. Currently, all your notebooks are stored in the directory `/home/ingavdb/workspace/`.