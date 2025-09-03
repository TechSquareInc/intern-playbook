# Learning Vi/Vim

*Vi (and its improved version Vim) is a modal text editor used in many Unix-based systems. This guide introduces the basic concepts and commands you need to start using `vi` or `vim`*.

---

## Opening a File

To open or create file use `vim <filename>`. If the file doesn't exist, it will be created when you save it.

## Modes in Vim

`vim` is a modal editor, which means it has different modes for different tasks.
- **Normal mode:** Vim's default mode allows navigation and issuing commands.
- **Insert mode:** Type and edit text
- **Visual mode:** Select text
- **Command-line mode:** Save, quit, search, etc.

### Switching Modes

| **Mode** | **Enter Mode** | **Description** |
|:---------:|:----------------:|:----------------:|
|Normal   |(deafult on start)|Move around, delete, copy, etc.|
|Insert | i, I, a , A, o O | Type text|
|Visual | v| Select Text|
|Command-line| : | Enter commands (save, quit, etc.)|

Press `Esc` to return to Normal mode from any other mode.

### Basic Navigation (Normal Mode)

- h - move left
- l - move right
- j - move down
- k - move up
- 0 - move to the beginning of the line
- $ - move to the end of the line
- G - move to the end of the file
- gg - move to the start of the file
- w - move forward a word
- b - move backward a word
### Editing Text

- i - insert before cursor
- a - append after cursor
- A - append text at the end of current line
- o - open a new line below
- O - open a new line above

### Saving and Quitting (Command-Line Mode)

Press `:` in Normal mode to enter the command line, then:
- :w - save(write)
- :q - quit
- :wq - save and quit
- :q! - quit without saving
- :x - save and quit (like :wq)

### Deleting and Undoing
- x - delete the character under the cursor
- dd - delete the current line
- (#)dd - delete given number of lines
- d$ - delete from the cursor to the end of line
- dw - delete word
- d2w - delete 2 words
- cw - change word
- ci( - change inside parenthesis
- u - undo
- `Ctrl` + r - redo

### Copy, Paste, and Yank
- yy - yank (copy) current line
- p - paste after the cursor
- P - paste before the cursor

### Searching
- ./word - search forward for "word"
- ?/word - search backward for "word"
- n - repeat search in same direction
- N - repeat in opposite direction

---
## Resources
- [VimGenius](http://www.vimgenius.com/): increase your speed and improve your muscle memory
- [`vimtutor`](https://vimschool.netlify.app/introduction/vimtutor/): an interactive tutorial. To run Vim Tutor, just call the command `vimtutor`
- [OpenVim](https://openvim.com/): an interactive tutorial available through your browser
- [Vim Adventures](https://vim-adventures.com/): learn Vim while playing a game
- [Learn Vimscript the Hard Way](https://learnvimscriptthehardway.stevelosh.com/): a book for Vim users who want to learn how to customize Vim. Before reading you should be comfortable editing text in Vim and know certain terms like "buffer," "window," and "insert mode."
- [Vim Cheatsheet](https://devhints.io/vim): commonly used keystrokes for easy reference
