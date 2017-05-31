## Text Editing with VIM

VIM is a text editor used on Linux file systems.

Open a file (or create a new file if it does not exist):
```
$ vim file_name
```

There are two "modes" in VIM that we will talk about today. They are called "insert mode" and "normal mode". In insert mode, the user is typing text into a file as seen through the terminal (think about typing text into TextEdit or Notepad). In normal mode, the user can do other things like save, quit, cut and paste, find and replace, etc. (think about clicking the menu options in TextEdit or Notepad). The two main keys to remember to toggle between the modes are `i` and `Esc`.

Entering VIM insert mode:
```
> i
```

Entering VIM nodmal mode:
```
> Esc
```

Navigating a file:
```
arrow keys	move up, down, left, right

	  h	move left
	  j	move down
	  k	move up
	  l	move right

    Ctrl+u	page up
    Ctrl+d	page down

	  0	move to beginning of line
	  $	move to end of line

	 gg	move to beginning of file
	  G	move to end of file
	 :N	move to line N
```

Deleting, copying, and pasting text:
```
	  x	delete letter under the cursor

	 dw	delete word
	 dd	delete line
	5dd	delete 5 lines
	 d$	delete until the end of the line
	 dG	delete until the end of the file

	 yy	copy line
      10yy	copy 10 lines
	 yG	copy until the end of the file
	  p	paste copied line below
	  P	paste copied line above
```

Searching for text:
```
	  /pattern	search for pattern

		  n	go to next hit of pattern
		  N	go to previous hit of pattern

	  /UpArrow	look through search history

    :set hlsearch	highlight search results
  :set nohlsearch	turn off highlight search results
```

The command line interface:
```
			  :	bring up command line at bottom
			 :N	move to line N

     :%s/find/replace/g	search through the file and replace
				all instances of ‘find’ with ‘replace’

    :%s/find/replace/gc	search through the file and replace
				all instances of ‘find’ with ‘replace’
				(but check with user first)

	 :read file_name	open the contents of file_name into
				this file
```


Saving and quitting:
```
			 :q	quit editing the file
			:q!	quit editing the file without saving

			 :w	save the file, continue editing
			:wq	save and quit

			 ZZ	Shortcut to save and quit
```


Other useful things to know:
```
	  u	Undo last change
    Ctrl+r	Reverse the last undo
	  .	Repeat the last change

	  o	Start insert mode below current line
	  O	Start insert mode above current line
```

For more information, see:
http://openvim.com/
http://vim-adventures.com

Or on the command line, type:
```
$ vimtutor
```



Previous: [Miscellaneous Commands](intro_to_linux_07.md) | Return to [Agenda](../index.md)

