# 📺 Using Screen and Tmux

*Brief introduction to Linux multiplexers like `screen` and `tmux`.*

---

## Introduction

`tmux` and `screen` are terminal multiplexers. This means that both are command line utilities that let you run multiple shell sessions in one terminal, detach and reattach to sessions, and keep long-running tasks alive (even after SSH dissconnection). This can be especially useful when working on remote servers. The two of them perform the same job, however in different ways, and you'll find that some tasks work better in one versus the other.

### `screen` Basics

- **Installation:** `sudo yum install screen`
- **Start a New Session:** `screen`
- **Start a New Session and Give it a Name:** `screen -S mysession`
- **Detach from a Session:** `Ctrl` + `A`, then `D`
- **List Sessions:** ` screen -ls`
- **Reattach to a Session:** `screen -r mysession` or if there is only one session run `screen -r`
- **Kill a Session:** from within a session `Ctrl` + `A`, then type `:quit`. From outside of a session `screen -X -S mysession quit`

### `tmux` Basics

- **Installation:** `sudo yum install tmux`
- **Start a New Session:** `tmux`
- **Start a New Sessions and Give it a Name:** `tmux new -s mysession`
- **Detach from a Session:** `Ctrl` + `B`, then `D`
- **List Sessions:** `tmux ls`
- **Reattach to a Session:** `tmux attach -t mysession`
- **Kill a Session:** `tmux kill-session -t mysession`

### Useful Tmux Shortcuts:

Use the prefix `Ctrl` + `B`

|**Action**|**Keys**|**Desscription**|
|:--------:|:------:|:--------------:|
|Split pane vertical|"|Split window top/bottom|
|Split pane horizontal|%|Split window left/right|
|Switch pane|Arrow keys|Move between panes|
|Create new window|c|Like creating a new tab|
|Switch windows|n/p|Next/previous window|
|List windows|w|Shows menu of windows|
|Rename window|,|Renmae current window|
|Close pane/window|exit|Just type exit|

## Choosing Between `screen` and `tmux`

Generally, `screen` is a more basic, limited, and minimal screen multiplexer. It offers some customization and is generally easier to use. However, `tmux` is highly customizable and offers more advanced pane and window management, and scripting support. A more detailed analysis of the two can be found [here](https://linuxhint.com/tmux_vs_screen/).

## Resources
- [Customize `tmux`](https://hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf/) make tmux pretty and usable
- [`tmux` Cheatsheet](https://tmuxcheatsheet.com/) guide for easy reference
- [`tmux` Manual](https://github.com/tmux/tmux/wiki/Getting-Started) indepth guide to using `tmux`
- [`screen` Basic Usage](https://aperiodic.net/screen/appearance) basic usage guide for `screen`
- [`screen` Manual](https://www.gnu.org/software/screen/manual/screen.html) complete and indepth `screen` guide
- [Get the Most out of `screen`](https://www.poweradmin.com/blog/how-to-get-the-most-out-of-the-linux-screen-command/) short guide with some customization options
- [Sharing Sessions for `tmux` and `screen`](https://www.howtoforge.com/sharing-terminal-sessions-with-tmux-and-screen)
