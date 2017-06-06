# Best Practices in Data Management and collaboration

### Course Objectives

This course is designed as an introduction to managing data on high performance computing clusters. It is intended to teach users to be self-sufficient and proactive in managing their own data in order to (1) increase their productivity, (2) maximize the usage of the existing storage, (3) decrease accidental or unintentional data loss, and (4) prevent disruption of the file system or compute nodes to the point where it may affect others. This course is intended for people who have beginner to intermediate familiarity with a command line interface, and have active accounts on a TACC HPC cluster.

This course is divided into four modules:

 1. [Overview of HPC Data Management](#mod1)
 2. [Navigating a File System](#mod2)
 3. [Moving and Backing up Data](#mod3)
 4. [Tips and Tricks for Maximizing File System Usage](#mod4)


### Instructional Objectives

This course should be taught in a room equipped with computers (or attendees with laptops) and internet access. Attendees should also have an existing allocation on a TACC resource. Attendees without an allocation can still participate in most components if they have a Mac / Linux laptop, or a Windows laptop with Putty installed and access to a Linux server.


### Specific Learning Objectives


[Module 1](data_management_01_01.md)
<table><tbody>
<tr><th><a name="mod1"></a>Module 1: Overview of HPC Data Management</th></tr>
<tr><td></td></tr>
<tr><th> <strong>Topics covered in this module:</strong> </th></tr>
<tr><td><ul><li> Why do we need best practices in data management? </li><li> Types of file systems used in HPC (NFS, GPFS/Lustre, LTFS, RAID). </li><li> Specific examples of storage infrastructures (TACC Stockyard, Ranch, Corral, WORK, SCRATCH). </li><li> Active vs. inactive data. </li><li> Staging data for compute, analysis, long term storage. </li></ul> </td></tr>
<tr><th> <strong>Attendees should be able to...</strong> </th></tr>
<tr><td><ul><li> List multiple reasons for good data management. </li><li> Describe the similarities and differences of distributed and parallel file systems. </li><li> Determine whether data is backed up or vulnerable. </li><li> Differentiate between active and inactive data. </li><li> Identify the appropriate storage spaces for data at different stages of its life cycle. </li></ul> </td></tr>
</tbody></table>

<br>

[Module 2](data_management_02_01.md)
<table><tbody>
<tr><th><a name="mod2"></a>Module 2: Navigating a File System </th></tr>
<tr><td></td></tr>
<tr><th> <strong>Topics covered in this module:</strong> </th></tr>
<tr><td><ul><li> Introduction to file system limitations (file size, number of files / inodes). </li><li> Determining the size and age of a file. </li><li> Determining the size of a directory, local disk usage (`du, du -h`). </li><li> Total amount of free disk space (`df, df -h`). </li><li> Checking your quota (`quota, lfs quota`). </li></ul></td></tr>
<tr><th> <strong>Attendees should be able to...</strong> </th></tr>
<tr><td><ul><li> Recognize file size and number limitations for a given file system. </li><li> Measure and report the size and age of a file and directory. </li><li> Measure and report disk usage. </li><li> Measure and report the total amount of free disk space. </li><li> Find different storage system mounted to a HPC cluster. </li><li> Determine their disk quota for various file systems. </li></ul></td></tr>
</tbody></table>

<br>

[Module 3](data_management_03_01.md)
<table><tbody>
<tr><th><a name="mod3"></a>Module 3: Moving and Backing up Data</th></tr>
<tr><td></td></tr>
<tr><th> <strong>Topics covered in this module:</strong> </th></tr>
<tr><td><ul><li> How old is your data and when is it time to archive it? </li><li> Zipping and archiving files and directories (`gzip, gzip -r9, gunzip, tar -czf, tar -xzf`). </li><li> Transferring data from point to point (`rsync, scp, sftp, WinSCP`). </li><li> Staging data on Ranch tape filesystem for archiving. </li></ul></td></tr>
<tr><th> <strong>Attendees should be able to...</strong> </th></tr>
<tr><td><ul><li> Judge whether it is appropriate to keep active or archive data. </li><li> Zip and unzip files with gzip / gunzip. </li><li> Compress and extract archives with tar. </li><li> Transfer data efficiently between systems. </li><li> Stage data on a tape file systems for transferring to and from. </li></ul></td></tr>
</tbody></table>

<br>

[Module 4](data_management_04_01.md)
<table><tbody>
<tr><th><a name="mod4"></a>Module 4: Tips and Tricks for Maximizing File System Usage</th></tr>
<tr><td></td></tr>
<tr><th> <strong>Topics covered in this module:</strong> </th></tr>
<tr><td><ul><li> Best practices in directory organization; dates and file names. </li><li> Get rid of duplicate copies of data and duplications within data (dedupe). </li><li> Share files with colleagues instead of duplicating them (permissions - `chmod`, `chown`, `chgrp`; access control lists; `ln`). </li><li> Don’t install common software in your home directory. </li></ul></td></tr>
<tr><th> <strong>Attendees should be able to...</strong> </th></tr>
<tr><td><ul><li> Differentiate organized vs. unorganized data. </li><li> Describe strategies to keep data well organized; especially in the context of job submission. </li><li> Remove duplicate copies of data where appropriate. </li><li> Set the correct permissions for sharing data where appropriate. </li></ul></td></tr>
</tbody></table>


<br>

Next: [Data Management](data_management_01_01.md) | UP: [Data Management Overview](data_management.md) | Top: [Course Overview](../../index.md)

<br>
&copy; 2017 Texas Advanced Computing Center
