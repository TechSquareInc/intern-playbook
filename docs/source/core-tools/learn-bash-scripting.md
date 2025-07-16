# 📜 Learn Bash Scripting

*Bash is a Unix shell and command language*

---

## What is Bash?

Bash (Bourne Again SHell) is a command-line interpreter that executes commands from a terminal or a file. Bash scripts are plain text files that contain a series of commands to be executed sequentially. Bash scripting allows you to automate tasks in Unix-like systems by writing a series of commands in a script file.

## Learning Bash

**1. Creating a Bash Script**

A bash script is simply a text file with executable commands. By convention, scripts have a `.sh` extension. An basic example of a bash script would look like:
```bash
#! /bin/bash
echo "Hello, world!"
```
- The first line `#!/bin/bash` is called a shebang. It tells the system to use Bash to execute the script.
- The second line is a command `echo` which prints text to the screen. 

**2. Saving and Running the Script**

1. Save the file with the `.sh` extension (example, `hello.sh`)
2. Make it executable by modifying the files permissions
```bash
chmod +x hello.sh
```
3. Run the script by calling 
```bash
./hello.sh
``` 
or 
```bash
sh hello.sh
```

### Bash Script Basics

#### Variables
```bash
name="Chloe"
echo "Hello, $name"
```
- Don't use spaces around the = when assigning value to a variable
- Use $ to reference the variable

#### User Input
```bash
read -p "Enter your name: " user_name
echo "Welcome, $user_name!"
```

#### Conditionals
```bash
if [ "$name" = "Chloe" ]; then
  echo "That's you!"
else
  echo "That's not me!"
fi
```

#### Loops
**For loop:**
```bash
for i in 1 2 3
do
  echo "Number $i"
done
```

**While loop:**
```bash
count=1
while [ $count -le 3 }
do
  echo "Count is $count"
  count=$((count +1))
done
```

#### Functions
```bash
greet() {
  echo "Hi, $1!"
}

greet "Chloe"
```

#### Best Practices
- Use meaningful variable names.
- Always quote your variables (`"${var}"`) when calling them to prevent issues with spaces.
- Include comments to explain your code:
```bash
# This is a comment
```

### Quality of Life Improvements

The default editor in bash for most linux systems is [nano](https://www.nano-editor.org/dist/v2.2/nano.html). [Vim/Vi](https://linux.die.net/man/1/vi) is an editor that can be especially useful for editing programs like bash scripts. Generally speaking, Vim is a more intuitive text editor, and will likely save you time and sanity when editing text files. You can ask your Linux system to default your editor to vim by calling `export EDITOR=vim`. Additionally, if you want to take things a step further, you can edit your commands with vim keybindings directly in the command line `set -o vi` and if you don't like this change you can always revert back `set -o emacs`. Most `.bashrc` configs come with `ll` being an alias to `"ls -l"`, but if it's not already set, you can add this alias, or other aliases, to the `.bashrc` file `alias ll="ls -l"`.

### Challenge
[BashBlaze: 7 Days of Bash Scripting](../intern-tasks/7-days-of-bash-scripting)
 
### Resources
- [Learn Shell](https://www.learnshell.org/): an interactive way to learn Bash basics.
- [Bash Scripting Tutorial](https://www.freecodecamp.org/news/bash-scripting-tutorial-linux-shell-script-and-command-line-for-beginners/): A beginner's guide to Linux shell script and command line.
- [GNU Bash Manual](https://www.gnu.org/software/bash/manual/bash.html): an all in one comprehensive Bash guide.
- [HackerRank Shell](https://www.hackerrank.com/domains/shell): practice your Bash knowledge by solving challenges.
- [learnyoubash](https://github.com/denysdovhan/learnyoubash): a work shop based on the [bash-handbook](https://github.com/denysdovhan/bash-handbook).
- [Nano vs Emacs vs Vim](https://www.redhat.com/en/blog/3-text-editors-compared): A "pro" position on each text editors features.
- [Shell Style Guide](https://google.github.io/styleguide/shellguide.html#when-to-use-shell): A more advance look at Bash shell scripting.
