## Text Editing with VIM

VIM is a text editor used on Linux file systems.

Open a file (or create a new file if it does not exist):
```
$ vim file_name
```

There are two "modes" in VIM that we will talk about today. They are called "insert mode" and "normal mode". In insert mode, the user is typing text into a file as seen through the terminal (think about typing text into TextEdit or Notepad). In normal mode, the user can perform other functions like save, quit, cut and paste, find and replace, etc. (think about clicking the menu options in TextEdit or Notepad). The two main keys to remember to toggle between the modes are `i` and `Esc`.

Entering VIM insert mode:
```
> i
```

Entering VIM nodmal mode:
```
> Esc
```

A summary of the most important keys to know for normal mode are (more on your cheat sheet):
```
# Navigating the file:
  
arrow keys        move up, down, left, right
    Ctrl+u        page up
    Ctrl+d        page down
 
         0        move to beginning of line
         $        move to end of line
 
        gg        move to beginning of file
         G        move to end of file
        :N        move to line N
  
# Saving and quitting:
 
        :q        quit editing the file
        :q!        quit editing the file without saving
 
        :w        save the file, continue editing
        :wq        save and quit
```


For more information, see:
  * [http://openvim.com/](http://openvim.com/)
  * [http://vim-adventures.com/](http://vim-adventures.com/) 
  * Or type on the command line: `vimtutor`

### Exercise

1. Navigate to the `Lab03` directory.
2. Open up the file called `tutorial.txt` and follow the instructions within.
3. Create a new file called `my_name.txt`, write your name within the file, save and quit, then print the contents of the file to screen.

[Click here for solution](intro_to_linux_08_solution.md)

### Review of Topics Covered

| Command         | Effect     |
|-----------------|------------|
| `vim file.txt`  | open "file.txt" and edit with `vim` |
| `i`             | toggle to insert mode |
| `<Esc>`         | toggle to normal mode |
| `<arrow keys>`  | navigate the file |
| `:q`            | quit editing the file |
| `:q!`           | quit editing the file without saving |
| `:w`            | save the file, continue editing |
| `:wq`           | save and quit |

Previous: [Miscellaneous Commands](intro_to_linux_07.md) | Top: [Course Overview](../../index.md)

