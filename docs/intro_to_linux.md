# Introduction to Linux

### Course Objectives

This course is designed to introduce skills required to perform computational research in the life sciences. Attendees will learn and practice commands in a Linux terminal, the text editor VIM, and basic shell scripting. This material is intended for people who have little to no experience with a command line interface, but intend to use a Linux workstation or HPC cluster for life science research.

This course is divided into two modules:

 1. [Linux Command Line Basics](#mod1)
 2. [Text Editing with VIM](#mod2)

### Instructional Objectives

This course is taught as an interactive workshop. Attendees will actively engage in course discussion, and participate with working examples in a Linux terminal. As such, it is necessary that attendees have access to a command line interface for the course. It should be taught in a room equipped with computers and internet access. Rooms not equipped with computers will work if the attendees bring their own laptops and have internet access. Attendees should also have an existing allocation on a TACC resource. Attendees without an allocation can still participate in most components of the workshop if they have a Mac / Linux laptop, or a Windows laptop with Putty installed and access to a Linux server.


### Specific Learning Objectives

| <a name="mod1"></a>Module 1: Linux Command Line Basics |
| --- |
| |
| **Topics covered in this module:** |
| <ul><li> Brief introduction to the Linux operating system. </li><li> Looking and moving around (`pwd, ls, mkdir, cd, rmdir`). </li><li> Creating and manipulating files (`touch, rm, mv, cp, vim`). </li><li> Looking at the contents of files (`cat, more, less, head, tail`). </li><li> More files commands (`ln, chmod, grep, tar, gzip`). </li><li> Network and file transfers (`hostname, whoami, ssh, scp, rsync`). </li><li> Miscellaneous commands (`man, which, diff, df, du, date, history, logout`). </li><li> Shortcuts (`Tab, Up Arrow, Ctrl+c, Ctrl+d, ./, ../, ~/, >, >>, *, |, &`). </li></ul> |
| **Attendees should be able to...** |
| <ul><li> List benefits and capabilities of a command line interface. </li><li> Use all of the commands covered in this module. </li><li> Find documentation for unknown commands and flags. </li></ul> |
| **Assessment activities:** |
| <ul><li> `Lab01.tar:` Naming and renaming directories for better organization. </li><li> `Lab02.tar:` Exploring large files (word lists and fasta). </li><li> `Lab03.tar:` Determine how to use previously unknown commands. </li></ul> |

<br>

| <a name="mod2"></a>Module 2: Text Editing with VIM |
| --- |
| |
| **Topics covered in this module:** |
| <ul><li> Switching back and forth between insert mode (IM) vs. normal mode (NM) (`i, o, O, Esc`). </li><li> IM: Entering text as a typical text editor. </li><li> NM: Navigating a file (`<arrow keys>, hjkl, 0, $, gg, G, Ctrl+u. Ctrl+d`). </li><li> NM: Deleting, copying, and pasting text (`x, dw, dd, yy, p, P, <number><command>`). </li><li> NM: Searching for text (`/pattern, n, N`). </li><li> NM: The command line (`:, :<line number>, :%s/find/replace/gc, :read <file>`). </li><li> NM: Saving and quitting (`:w, :wq, :q, :q!`). </li><li> NM: Other useful things to know (`u, Ctrl+r, .`). </li></ul> |
| **Attendees should be able to...** |
| <ul><li> Open, edit, and save documents with VIM. </li><li> Switch back and forth between insert mode and normal mode. </li><li> Navigate to different parts of a file quickly. </li><li> Search for a specific string of text. </li><li> Find and replace text. </li></ul> |
| **Assessment activities:** |
| <ul><li> `Lab04.tar:` Curating gene sequence files for analysis. </li><li> Learn by practice! Dive headfirst into Module 3! </li><li> Other practice tools available: `vimtutor`, vim-adventures.com, openvim.org. </li></ul> |

<br>
&copy; 2017 Texas Advanced Computing Center


