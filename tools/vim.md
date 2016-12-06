# Vim
I'm not really a vim user, seems a bit too complex for the sake of complex. But sometimes I use it.

## General
`.vimrc` file is used to store configurations. it is located in your home directory
List of [special keys](http://vimdoc.sourceforge.net/htmldoc/intro.html#%3CNul%3E)

## Modes
Vim is a modal editor, to use the editor you need to be in the correct mode
* `CTRL+C`: command mode
* Normal mode default mode used to navigate around the file
* i - insert mode
* v - visual mode, used to select blocks of text from a file, click `shift+v` to enter visual line mode
  - use hjkl to move around in visual mode
* a - append mode
* ctrl+ww - switch to another panel
* ctrl+w<hjkl> - move to split left, right ...etc
* ctrl+w| - to expand a split
* ctrl+w= - set the splits to an equal width

## Key commands
From command mode
* use the **hjkl** to move up down left and right
* use **w** to move to the next word and **b** to move to the previous
* `shift + v` - visual line mode
* **o** - add a new line
* **gg** - start of file
* **G** - end of file
* **0** - move to start of line
* `$` - end of the line
* **x** - remove char
* **y** - yank (copy) text, its not copied to the clipboard though
* **yy** - copy the line
* **p** - paste
* **d** - cut/delete
* **dd** - cut/delete a line
* `shift+dd` - remove the line but leave the space
* **cw** - replace a word and change to insert mode
* **ew** - remove a word and stay in normal mode
* **cit** - delete content within a context - ie html inner text
* `ci+<character>`: context delete, ie `ci"` will delete the text in quote marks, `ci{` will delete text in braces
* **bd** - buffer delete -> close file
* `/<search>` - search for the term we specify, use n to move to the next occurence in the file
* **zz** - set the current line as the centre of the screen

## Other commands
* :help option list - list all the options
  - guiptions
* :syntax on/off
* :set number / :set nonumber
* :e filename - opens a file for editing
  - :e . - shows the current dir
* :pwd - show the current working dir
* :colorscheme - list all the available color schemes
* :so % - source the current file (reload)
* :u - undo
* `:w` - write the changes to the file
  - `:w filename` - save file with a new name
* `:x` - write the changes and exit
* :tabedit / :tabclose - open and close a new tab
* :nohlsearch - turn off search results highlighting
* :sp / :vsp - horizontal / veritcal split
* :ls - show all open buffers
* :bp - previous buffer
  - :b<1,2..> - move to buffer number ..
* :sh - open a shell

## Shortcuts
* Swap 2 lines: `:<line number 1>mo<line number 2>`
    
## Keys
* <cr> - carriage return (enter)
* <Leader> - reference the default leader key (default is \)

## vundle
used to manage vim plugins
config file stored at `~/.vim/plugins.vim`
:PluginInstall - show all the installed plugins

* CTRL+P - quickly switch files
  - CtrlPBufTag - show the functions we have defiend
  - CtrlPMRUFiles - show the most recently used files
* NERDTree: tree viewer
  - **NERDTreeToggle** - show / hide the nerdtree view
  - [cheatlist](https://www.cheatography.com/stepk/cheat-sheets/vim-nerdtree/)
* vim-vinegar: nice file browser
  - **-** - opens up the current dir
  - **d** - create new dir
  - **D** - delete dir
  - `%` - new file
