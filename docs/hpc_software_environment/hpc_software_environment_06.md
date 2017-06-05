## Sharing an Application

Now that you have installed Tophat in your account and confirmed that it is working, you may want to share it with other members of your lab, or with the wider community. In order to do that, we must change "permissions" on the Tophat installation folder so that other Lonestar5 users can see it.

Navigate to your `apps` directory on Lonestar and find your `tophat` folder:
```
$ cd /work/03439/wallen/lonestar/apps
$ ls -l
drwx------  3 wallen G-815499       4096 Jun  2 14:16 tophat/
```

The `tophat` directory, containing all executables, currently has permissions set such that only the owner `wallen` can read, write, and execute. The group (those with access to group id `G-815499`) and all others on the file system have no access at this time. To open up this directory for others to see, use `chmod`:
```
$ chmod -R g=u-w tophat/
$ ls -l
drwxr-x---  3 wallen G-815499       4096 Jun  2 14:16 tophat/
```

The `-R` flag is used to change permissions recursively (all folders and files within `tophat`). The `g=u-w` directive is used to give members of the same Linux group the same permissions as the owner, minus write permissions. To do the same thing but for all others on Lonestar5, do:
```
$ chmod -R go=u-w tophat/
$ ls -l
drwxr-xr-x  3 wallen G-815499       4096 Jun  2 14:16 tophat/
```

Notice the new `o` in `go=u-w`. The permissions have been changed for all files within the `tophat` directory. But, we are not done quite yet. We need to walk up and change permissions on the `apps`, `lonestar`, and `wallen` directories as well:
```
$ cd ../
$ pwd
/work/03439/wallen/lonestar
$ chmod go=u-w apps/
 
$ cd ../
$ pwd
/work/03439/wallen
$ chmod go=u-w lonestar/
 
$ cd ../
$ pwd
/work/03439
$ chmod go=u-w wallen/
```

Notice we did not do recursive `-R` this time. Test this by checking with your neighbor. You should be able to list files in each other's `tophat` directories.

To undo the changes, walk backwards and issue:
```
$ chmod go-rwx directory/
or
$ chmod -R go-rwx directory/
```

The `go-rwx` directive will remove all read, write, and execute permissions from everyone except the owner from a folder called `directory/`. It may be good practice to put all files you want to share in one central location to limit the number of places you make accessible. For example, I only have opened permissions in one directory on my own account:
```
$ ls -l /work/03439/wallen/public
```

Previous: [Profiling an Application](hpc_software_environment_05.md) | Next: [Making Modules](hpc_software_environment_07.md) | Top: [Course Overview](../../index.md)

