# Vim
I'm not really a vim user, seems a bit too complex for the sake of complex. But sometimes I use it.

## General
`.vimrc` file is used to store configurations. it is located in your home directory

## Modes
Vim is a modal editor, to use the editor you need to be in the correct mode
* `CTRL+C`: command mode
* Normal mode default mode used to navigate around the file 
* i - insert mode
* v - visual mode, used to select blocks of text from a file, click `shift+v` to enter visual line mode
  - use hjkl to move around in visual mode
* a - append mode
* ctrl+ww - switch to another panel 

## Key commands
From command mode
* use the `hjkl` to move up down left and right
* use `w` to move to the next word and `b` to move to the previous
* `shift + v` - visual line mode
* `w` - write the changes to the file
* `x` - write the changes and exit
* `y` - yank (copy) text, its not copied to the clipboard though
* `yy` - copy the line
* `p` - paste
* `d` - cut/delete
* `dd` - cut/delete a line
* `shift+dd` - remove the line but leave the space
* `cw` - replace a word and change to insert mode
* `ew` - remove a word and stay in normal mode
* `cit` - delete content within a context - ie html inner text
* `ci+<character>`: context delete, ie `ci"` will delete the text in quote marks, `ci{` will delete text in braces
* `bd` - buffer delete -> close file
* `/<search>` - search for the term we specify, use n to move to the next occurence in the file
* `zz` - set the current line as the centre of the screen

## Other commands
* :help option list - list all the options
  - guiptions
* :syntax on/off
* :set number / :set nonumber
* :e filename - opens a file for editing
* :pwd - show the current working dir
* :colorscheme - list all the available color schemes
* :so % - source the current file (reload)
* :u - undo
* :tabedit / :tabclose - open and close a new tab
* :nohlsearch - turn off search results highlighting

## Keys
* <cr> - carriage return (enter)
* <Leader> - reference the default leader key (default is \)
