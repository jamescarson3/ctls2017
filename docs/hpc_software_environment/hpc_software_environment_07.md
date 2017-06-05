## Making Modules

The easiest way to share an application with your colleagues (or others) is to wrap up that application in a module. Just like the central module system on Lonestar5, each user may have their own module folder(s) to easily load or unload custom applications. The first step is to create a module folder in an area that you do not mind making public. Here, we will do this in the `$WORK/apps` folder, but you may choose to do this somewhere else:
```
$ cd $WORK/apps
$ pwd
/work/03439/wallen/lonestar/apps
$ ls                              # my installation of tophat is in this same folder
$ mkdir -p modulefiles/tophat     # check the man page if you do not know what -p does
```

The easiest way to make a new module file is to use an existing module file as a template. A good example template is the module used for the application `bowtie/2.2.6`. You can find that here:
```
$ cd /opt/apps/modulefiles/bowtie
$ ls
1.1.2.lua  2.2.6.lua
```

In that directory, two files exist - one for each available version of `bowtie`. Print the contents of `2.2.6.lua` to screen:
```
$ cat 2.2.6.lua
help (
[[
The bowtie module file defines the following environment variables:
TACC_BOWTIE_DIR and TACC_BOWTIE_SCRIPTS for the location of the tacc-bowtie
distribution. Documentation can be found online at http://bowtie-bio.sourceforge.net/bowtie2/

NOTE: Bowtie2 indexes are not backwards compatible with Bowtie1 indexes.

This module provides the bowtie2, bowtie2-align, bowtie2-build, and bowtie2-inspect binaries + scripts

Version 2.2.6

]])

whatis("Name: Bowtie")
whatis("Version: 2.2.6")
whatis("Category: computational biology, genomics")
whatis("Keywords: Biology, Genomics, Alignment, Sequencing")
whatis("URL: http://bowtie-bio.sourceforge.net/bowtie2/")
whatis("Description: Ultrafast, memory-efficient short read aligner")

setenv("TACC_BOWTIE_DIR",              "/opt/apps/bowtie/2.2.6")
setenv("TACC_BOWTIE_SCRIPTS", pathJoin("/opt/apps/bowtie/2.2.6","scripts"))
prepend_path("PATH",                     "/opt/apps/bowtie/2.2.6")

prereq("perl")
```

The first half of the file is a plain text description of the application, `bowtie`. The second half contains some descriptions for the `module whatis` directive, a few lines of changes to environment variables, and finally one prerequisite module, `perl`. To use this as a template, first copy it to your new module file directory, and rename it to match the Tophat version:
```
$ cp 2.2.6.lua $WORK/apps/modulefiles/tophat/2.1.1.lua
```

Next, we need to edit the file:
```
$ cd $WORK/apps/modulefiles/tophat
$ vim 2.1.1.lua
```

Change the text to the following:
```
help (
[[
This module is for a locally-installed version of tophat.

Version 2.1.1

]])

whatis("Name: tophat")
whatis("Version: 2.1.1")
whatis("Category: computational biology, genomics")
whatis("Keywords: Biology, Genomics, Alignment, Sequencing")
whatis("URL: https://ccb.jhu.edu/software/tophat/tutorial.shtml")
whatis("Description: A spliced read mapper for RNA-seq")

setenv("TACC_TOPHAT_DIR", "/work/03439/wallen/lonestar/apps/tophat/2.1.1")
prepend_path("PATH",      "/work/03439/wallen/lonestar/apps/tophat/2.1.1/bin")

prereq("bowtie/2.2.6")
prereq("boost/1.59")
prereq("intel/16.0.1")
```

I shortened the description a bit, and made sure to mention that this module is for a locally-installed version of Tophat. I also updated the whatis directives for Tophat. I defined an environment variable called `TACC_TOPHAT_DIR` to point to the Tophat install location, and I added the Tophat `bin` to the `PATH`. Finally, I defined a few prerequisites that we know must also be loaded for Tophat to work properly. Save and quit VIM with `:wq` once these changes are made.

There is an environment variable called `MODULEPATH` defined in your shell:
```
$ echo $MODULEPATH
```

This is the list of locations that the `module avail` or `module load` commands search through. To add this new module file directory to your `MODULEPATH`, we will use the `module use` command:
```
$ cd $WORK/apps/modulefiles
$ pwd
/work/03439/wallen/lonestar/apps/modulefiles
$ echo $PWD
/work/03439/wallen/lonestar/apps/modulefiles
$ module use $PWD
$ echo $MODULEPATH
```

Compare the contents of `MODULEPATH` before and after the `module use` command to make sure the expected changes are there. Use the `module save` command to make this change permanent. Try loading and unloading the module, checking your environment before and after, to make sure your new Tophat module is working as expected:
```
$ module avail         # is there a new category of modules available?
$ module avail tophat
$ module load tophat   # are the dependencies loaded?
$ which tophat
$ tophat --version
```

The final step is to modify the permissions of the module file (and parent directories) to share with your target group. For example:
```
$ cd /work/03439/wallen/lonestar/apps
$ chmod -R go=u-w modulefiles                  # this is assuming I already changed permissions above this dir
```

Then, you would need to just ask your colleagues to execute the following command to have access to your module:
```
$ module use /work/03439/wallen/lonestar/apps/modulefiles
```


If, for example, you want to install a custom version of an application that is already in the Lonestar5 central module system, you can still do so. Modify either the name of the application directory or the name of the `lua` file so that loading it does not conflict with the existing module file. For example, you could name the local module `tophat-wallen/2.1.1` so it is different from any other `tophat/2.1.1`.

Now, set permissions and try loading your neighbor's (or my) version of Tophat.




Previous: [Sharing an Application](hpc_software_environment_06.md) | Top: [Course Overview](../../index.md)

