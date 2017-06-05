## Installing an Application

Now we will try to install our own application from the web. We are going to try to install a spliced read mapper for RNA-seq called [Tophat](https://ccb.jhu.edu/software/tophat/tutorial.shtml).

The first thing to do is decide a good place to install the application. The `$WORK` file system on TACC resources is suitable. Navigate to the `$WORK` file system, and make a new directory called `apps`, where we can put all of the applications we install:
```
$ cd $WORK
$ pwd
/work/03439/wallen/lonestar
$ mkdir apps
$ cd apps
$ pwd
/work/03439/wallen/lonestar/apps
```

According to the Tophat documentation, we need `bowtie2` and `boost` are dependencies. Check your environment and load what we know we need for Tophat:
```
$ module load boost/1.59
$ module load bowtie/2.2.6
Lmod has detected the following error:  Cannot load module "bowtie/2.2.6" without these module(s)
loaded:
   perl
```

Whoops! We first need to load `perl` before we can load `bowtie`:
```
$ module load perl/5.22.1
$ module load bowtie/2.2.6
$ module list
Currently Loaded Modules:
  1) intel/16.0.1   2) cray_mpich/7.3.0   3) TACC/1.0   4) boost/1.59   5) perl/5.22.1   6) bowtie/2.2.6
```


We will use the `wget` command to download the Tophat source code straight from the web, and `tar` command to unpack the file. We also make a directory called `tophat/2.1.1` which is where the installation will go:
```
$ wget https://ccb.jhu.edu/software/tophat/downloads/tophat-2.1.1.tar.gz
$ tar -xvzf tophat-2.1.1.tar.gz
$ mkdir -p tophat/2.1.1
$ cd tophat-2.1.1
```

According to the Tophat documentation, it follows a standard installation scheme of `./configure`, `make`, `make install`. The first step checks your environment for all the right dependencies, the second step compiles the code, and the third step moves the appropriate binaries and libraries to your target install location. Try running the first step with a `--help` flag to see what information you can learn:
```
$ ./configure --help
```

A few things to note from the help text:
 * We cannot install into the default `/usr/local` folder, so we will have to specify our own prefix
 * We may try using the `--enable-intel64` flag since we are compiling with intel processors
 * We may need to specify the location of boost with the `--with-boost` flag, even though it is already in our path
 * There is a helpful list of environment variables at the bottom

Try to configure using the `--prefix` and `--enable-intel64` flags:
```
$ ./configure --prefix=/work/03439/wallen/lonestar/apps/tophat/2.1.1 \
              --enable-intel64
...
checking for boostlib >= 1.38.0... configure: error: We could not detect the
boost libraries (version 1.38 or higher). If you have a staged boost library
(still not installed) please specify $BOOST_ROOT in your environment and do not
give a PATH to --with-boost option.  If you are sure you have boost installed,
then check your version number looking in <boost/version.hpp>. See
http://randspringer.de/boost for more documentation.
```

It works for a little bit before giving the boost error above. Perhaps we do need to specify the boost path after all:
```
$ ./configure --prefix=/work/03439/wallen/lonestar/apps/tophat/2.1.1 \
              --with-boost=/opt/apps/intel16/boost/1.59 \
              --enable-intel64
```

This time it got all the way through the `./configure` step, except there is something funny in the summary text:
```
...
-- tophat 2.1.1 Configuration Results --
  C++ compiler:        g++ -Wall -Wno-strict-aliasing -g -gdwarf-2 -Wuninitialized  -mtune=nocona -O3  -DNDEBUG -I./samtools-0.1.18 -pthread -I/opt/apps/intel16/boost/1.59/include -I./SeqAn-1.4.2
  Linker flags:        -L./samtools-0.1.18 -L/opt/apps/intel16/boost/1.59/lib
  BOOST libraries:     -lboost_thread -lboost_system
  GCC version:         gcc (GCC) 4.9.3
  Host System type:    x86_64-unknown-linux-gnu
  Install prefix:      /work/03439/wallen/lonestar/training/apps/tophat/2.1.1
  Install eprefix:     ${prefix}
...
```

It looks like it is still trying to use gcc compilers, even though we have intel compilers loaded. This is where the environment variables come in. As a reminder:
```
$ ./configure --help
Some influential environment variables:
  PYTHON      python program
  CXX         C++ compiler command
  CXXFLAGS    C++ compiler flags
  LDFLAGS     linker flags, e.g. -L<lib dir> if you have libraries in a
              nonstandard directory <lib dir>
  LIBS        libraries to pass to the linker, e.g. -l<library>
  CPPFLAGS    (Objective) C/C++ preprocessor flags, e.g. -I<include dir> if
              you have headers in a nonstandard directory <include dir>
  CC          C compiler command
  CFLAGS      C compiler flags
  CXXCPP      C++ preprocessor
```

The contents of the variables we are interested in are empty:
```
$ echo $CC
$ echo $CXX
```

We can force Tophat to use the intel compilers by pointing those variables to the appropriate C and C++ compilers:
```
$ which icc
/opt/apps/intel/16.0.1.150/compilers_and_libraries_2016.1.150/linux/bin/intel64/icc
$ export CC=`which icc`
echo $CC
/opt/apps/intel/16.0.1.150/compilers_and_libraries_2016.1.150/linux/bin/intel64/icc
$ export CXX=`which icpc`
```

And, if you recall from before, Lonestar5 has nodes with different architectures. Now is our chance to specify a few extra compilation flags so that the binaries can run anywhere:
```
$ export CFLAGS="-xAVX -axCORE-AVX2"
$ export CXXFLAGS="-xAVX -axCORE-AVX2"
$ export LDFLAGS="-xAVX -axCORE-AVX2"
```


Configure one more time and make sure the output makes sense:
```
$ ./configure --prefix=/work/03439/wallen/lonestar/apps/tophat/2.1.1 \
              --with-boost=/opt/apps/intel16/boost/1.59 \
              --enable-intel64
...
-- tophat 2.1.1 Configuration Results --
  C++ compiler:        /opt/apps/intel/16.0.1.150/compilers_and_libraries_2016.1.150/linux/bin/intel64/icpc -Wall -Wno-strict-aliasing -g -gdwarf-2 -Wuninitialized  -mtune=nocona -O3 -xAVX -axCORE-AVX2 -DNDEBUG -I./samtools-0.1.18 -pthread -I/opt/apps/intel16/boost/1.59/include -I./SeqAn-1.4.2
  Linker flags:        -L./samtools-0.1.18 -L/opt/apps/intel16/boost/1.59/lib -xAVX -axCORE-AVX
  BOOST libraries:     -lboost_thread -lboost_system
  GCC version:         icc (ICC) 16.0.1 20151021
  Host System type:    x86_64-unknown-linux-gnu
  Install prefix:      /work/03439/wallen/lonestar/apps/tophat/2.1.1
  Install eprefix:     ${prefix}
...
```

This looks better. Finish with:
```
$ make                # compiles code
$ make install        # moves binaries into $WORK/apps/tophat/2.1.1
$ ls -l ../tophat/2.1.1/
$ ls -l ../tophat/2.1.1/bin
```

The `tophat/2.1.1/bin` directory should be filled with executables.

Previous: [Lonestar5 Basics](hpc_software_environment_02.md) | Next: [Testing an Application](hpc_software_environment_04.md) | Top: [Course Overview](../../index.md)

