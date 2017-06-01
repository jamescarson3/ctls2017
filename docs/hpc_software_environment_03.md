## Installing an Application

 2. Install an application (Tophat); ./configure, make, make install

# (requires bowtie 1 or 2  and boost >1.47)

```
module swap intel/16.0.1 gcc/5.2.0
module load boost/1.61.0

Currently Loaded Modules:
  1) TACC/1.0   2) git/2.7.1   3) gcc/5.2.0   4) boost/1.61.0
```



```
cd $WORK/lonestar/apps
wget https://ccb.jhu.edu/software/tophat/downloads/tophat-2.1.1.tar.gz
tar -xvzf tophat-2.1.1.tar.gz
mkdir -p tophat/2.1.1
cd tophat-2.1.1


./configure --prefix=/work/03439/wallen/lonestar/apps/tophat/2.1.1 --enable-intel64 --with-boost=/opt/apps/boost/1.61.0 --with-bam=/work/03439/wallen/lonestar/apps/samtools/1.3 LDFLAGS="-Wl,-rpath,$TACC_BOOST_LIB,-rpath,$GCC_LIB"

make BOOST_LDFLAGS="-L$TACC_BOOST_LIB -Wl,-rpath,$TACC_BOOST_LIB,-rpath,$GCC_LIB"
```


### Exercise

1. 

[Click here for solution](hpc_software_environment_03_solution.md)



Previous: [Lonestar5 Basics](hpc_software_environment_02.md) | Next: [Testing an Application](hpc_software_environment_04.md)

