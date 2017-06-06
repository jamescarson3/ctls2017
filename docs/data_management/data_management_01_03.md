### What are the disk/file system resources on TACC HPC systems?

  <center><img src="../../resources/HPC_Storage.png" style="height:300px;"></center>

* **A typical HPC system at TACC uses:**
  + `/home1`
    * LustreFS
    * 13 TB LS5, 524 TB Stampede
    * each user has 5 GB quota
    * ENV VAR: `$HOME`
  + `/scratch`
    * LustreFS
    * 7.5 PB
    * Unlimited quota, but **10 day limit**
    * ENV VAR: `$SCRATCH`
  + `/work`
    * LustreFS
    * 20 PB
    * each user has 1 TB quota
    * ENV VAR: `$WORK`
  + `/corral-repl`
    * GPFS/NFS
    * 6x2 PB
      + 6 PB in each of Austin and Arlington
    * typical quota: 5 TB but varies based on need
    * folder path provided upon allocation
      + `/corral-repl/TACC/bio/ECR`
  + RANCH TAPE Robot
    * LTFS
    * 160 PB
    * Unlimited quota
    * ENV VAR: `$ARCHIVER, $ARCHIVE`


### TACC HPC Storage systems?

<center><img src="../../resources/TACC_Ecosystem.png" style="height:300px;"></center>

* The `$WORK` filesystem on Stockyard helps knit TACC HPC Systems together
  + Files on `$WORK` are present on most systems.


<br>

Prev: [File Systems](data_management_01_02.md) | Next: [Active Data](data_management_01_04.md) | UP: [Data Management Overview](data_management.md) | Top: [Course Overview](../../index.md)
