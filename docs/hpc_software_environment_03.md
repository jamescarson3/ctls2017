## Installing an Application

 2. Install an application (Tophat); ./configure, make, make install

# (requires bowtie 1 or 2  and boost >1.47)


First find a good place to work:
```
$ cd $WORK
$ mkdir apps
$ cd apps
$ pwd
/work/03439/wallen/lonestar/apps
```

Check your environment and load what we know we need for Tophat:
```
$ module load boost/1.59
 
Currently Loaded Modules:
  1) intel/16.0.1   2) cray_mpich/7.3.0   3) TACC/1.0   4) boost/1.59
```


Download and unpack the file. We also make a directory called `tophat/2.1.1` which is where the installation will go::
```
$ wget https://ccb.jhu.edu/software/tophat/downloads/tophat-2.1.1.tar.gz
$ tar -xvzf tophat-2.1.1.tar.gz
$ mkdir -p tophat/2.1.1
$ cd tophat-2.1.1
```


Follow the installation steps according to the online instructions:
```
./configure --help
./configure --enable-intel64 --with-boost=/opt/apps/intel16/boost/1.59 --prefix=/work/03439/wallen/lonestar/apps/tophat/2.1.1
...
-- tophat 2.1.1 Configuration Results --
  C++ compiler:        g++ -Wall -Wno-strict-aliasing -g -gdwarf-2 -Wuninitialized  -mtune=nocona -O3  -DNDEBUG -I./samtools-0.1.18 -pthread -I/opt/apps/intel16/boost/1.59/include -I./SeqAn-1.4.2
  Linker flags:        -L./samtools-0.1.18 -L/opt/apps/intel16/boost/1.59/lib
  BOOST libraries:     -lboost_thread -lboost_system
  GCC version:         gcc (GCC) 4.9.3
  Host System type:    x86_64-unknown-linux-gnu
  Install prefix:      /work/03439/wallen/lonestar/training/apps/tophat/2.1.1
  Install eprefix:     ${prefix}
 
  See config.h for further configuration information.
  Email bug reports to <tophat.cufflinks@gmail.com>.
...
```

That is strange - it is still trying to use gcc to install, not icc like we want.
```
$ export CC=`which icc`
$ export CXX=`which icpc`
$ make clean
$ ./configure --enable-intel64 --with-boost=/opt/apps/intel16/boost/1.59 --prefix=/work/03439/wallen/lonestar/apps/tophat/2.1.1
...
-- tophat 2.1.1 Configuration Results --
  C++ compiler:        /opt/apps/intel/16.0.1.150/compilers_and_libraries_2016.1.150/linux/bin/intel64/icpc -Wa
ll -Wno-strict-aliasing -g -gdwarf-2 -Wuninitialized  -mtune=nocona -O3  -DNDEBUG -I./samtools-0.1.18 -pthread
-I/opt/apps/intel16/boost/1.59/include -I./SeqAn-1.4.2
  Linker flags:        -L./samtools-0.1.18 -L/opt/apps/intel16/boost/1.59/lib
  BOOST libraries:     -lboost_thread -lboost_system
  GCC version:         icc (ICC) 16.0.1 20151021
  Host System type:    x86_64-unknown-linux-gnu
  Install prefix:      /work/03439/wallen/lonestar/training/apps/tophat/2.1.1
  Install eprefix:     ${prefix}
 
  See config.h for further configuration information.
  Email bug reports to <tophat.cufflinks@gmail.com>.
...
```

This looks better. Finish with:
```
$ make
$ make install
```

### Exercise

1. 

[Click here for solution](hpc_software_environment_03_solution.md)



Previous: [Lonestar5 Basics](hpc_software_environment_02.md) | Next: [Testing an Application](hpc_software_environment_04.md)

