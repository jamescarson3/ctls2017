# Hands-On: Day 1

These excercises are intended to reinforce the material from Day 1 of the course
and provide practical ways to customize the Linux shell toward your own
preferences.

## Customizing your "Command Prompt"

In the Linux shell, all the text before where your cursor starts is generally
called the "command prompt".  That text is defined by a special environment 
variable called PS1. 

**Print PS1 to the screen using the echo command.**

The PS1 variable is just a *string*, and there are several special patterns
that just have meaning when building the command prompt:


* \u - username
* \h - short hostname (e.g "ls5" for "ls5.tacc.utexas.edu")
* \H - full hostname (e.g. "ls5.tacc.utexas.edu")
* \d - date in “Weekday Month Date” format
* \D{format} - the format is passed to strftime(3) and the result is inserted into the prompt string; an empty format results in a locale-specific time representation.
* \e - an ASCII escape character (alternately \033)
* \j - number of jobs currently managed by the shell
* \n - newline character (if you really want a multi-line command prompt)
* \t - current time in 24-hour HH:MM:SS format
* \T - current time in 12-hour HH:MM:SS format
* \@ - current time in 12-hour am/pm format
* \A - current time in 24-hour HH:MM format
* \w - current working directory
* \W - basename of the current working directory
* \! - the history number of this command
* \# - the command number of this command
* \$ - if the effective UID is 0 (i.e. you are root), a #, otherwise a $. This 
is commonly the last character of the command prompt.
* \xyz - the character corresponding to the octal number xyz
* \\ - a backslash
* \[ - begin a sequence of non-printing characters, which could be used to embed a terminal control sequence into the prompt
* \] - end a sequence of non-printing characters

What information is currently in your command prompt?
**Try changing something in your command prompt.**  All you need to do is set the
PS1 Variable to something new. For example:

```
export PS1="\u@\h:\w(\#) \$ "
```

In addition to these special patterns, you can use shell variables and run shell
commands to build your command prompt

I personally define colors as bash variables and then use them in my command prompt:

```
  # Colors
  White='\[\033[0m\]'             # White
  Bright_Red='\[\033[01;31m\]'    # Bright Red
  Green='\[\033[0;32m\]'          # Green
  Bright_Green='\[\033[1;32m\]'   # Bright Green
  Brown='\[\033[0;33m\]'          # Brown
  Yellow='\[\033[1;33m\]'         # Yellow
  Bright_Blue='\[\033[1;34m\]'    # Bright Blue
  Gray='\[\033[1;30m\]'
```

**Now try something like:**

```
export PS1="$Bright_Green\u@\h:\w(\#) \$$White "
```

By the way, what happens if you leave the `$White` off at the end?

You can also execute bash commands inside your command prompt by surrounding the command with $(). For example:

```
$(echo -e '\[\e[01;32m\]:)')
```

**Can you replace the \h portion of your command prompt with a `$(hostname)` command?** (just for fun... and then change it back)

Once you are happy with your command prompt, put it inside of your ~/.bashrc file so that it will be that way everytime you login.**  If you are following TACC's convention for organizing your startup scripts, there will likely be a section set aside for it.  Something like:

```
if [ -n "$PS1" ]; then

    # Put all your custom variables, functions, and PS1 here

fi
```

## Create a local *bin/* directory

As you work more and more in the shell, you will write short scripts that do handy things.  It is useful to have a place to put those handy scripts.  A common convention is to create a `bin` directory inside of your $HOME directory and put things there.

```
mkdir ~/bin
cd ~/bin
```

#### Make a Bash script

A script is just a special text file that has a few extra requirements:

1. The text is code that can be "interpreted" and executed
2. The file has **executable** permissions (so Linux is allowed to run it)
3. It is (optionally) in a directory that is part of your $PATH (otherwise you have to type in the directory too)

Let's start as simply as we can.  **Make a file called `whereami`**

```
touch whereami
```

Now open that file in your favorite text editor and put in these contents:

```
#!/usr/bin/env bash

pwd
```

The first line of this script is lovingly called the "shebang" line.  It tells Linux
what kind of script we wrote.  In this case, it is a "bash" script, but later we
will make a python script as well.  Letting Linux use the "env" tool to pick which bash
interpreter to use is considered best practice for portability.  For the 99% use case,
though, we could have equally put `#!/bin/bash`.

Everything after the shebang line is the code we want to execute.  In this case,
all we do is print the working directory.  A bit too simplistic to be extremely helpful,
but it's a good start.

Once you have your file, it's time for step 2.  Use `chmod` to make your file executable.

```
chmod +x ~/bin/whereami
```


#### Add it to your $PATH

To test your script, you can add the `~/bin` directory to your path and try it out.
To make sure the `~/bin` directory is always in your path, though, you need to add
it to your startup scripts (i.e. ~/.bashrc).

```
export PATH=$PATH:~/bin
```

The above command appends your `~/bin` directory to the path.  What would happen if
we "prepended" `~/bin` to the beginning?  Why or why not might you want to append vs.
prepend a path?

**Don't forget to update your ~/.bashrc file!**

## Bonus: Create a "Save your history" script

As a bonus, make a script that will save your history.  This can be extremely handy for remembering what you did in the past.  The requirements are that it must:

1. Create a "log file" that has the date in the name
2. Print some nice comment at the top of the file about the time it was created, the purpose of the file, or whatever you want
3. use the `history` command and "output redirection" to print your history to that file (or, say, the most recent 100 lines)


