# Terminal tutorials
* Text starting with a `#` are my comments; on git-bash they shouldn't do anything (and on cmd it might print an error at you).
* Lines starting with `$` are typed by the user into a bash terminal; don't type the `$`, it's already there
* Lines starting with `>` are typed by the user into a cmd terminal; don't type the `>`
* Lines without a `$`, `>`, or `#` are printed by the console
* Execute lines by typing them and hitting enter

## Getting help text
Putting this at the top as it's the main thing to help you.

CLI tools are scary to noobs because they don't know what to do. But if you have a tool name / command, you can ask it for help. This generally looks like executing `<toolname> --help`. However, for historical reasons and because Microsoft _had_ to be different, it's not always `--help`. Here's the checklist, querying `my_tool` for help, with my notes on lines with `#`
```bash
# Most universal:
> my_tool -h
# The linux, Python, and multiplatform standard:
# The two dashes are there for historical reasons at this point
> my_tool --help
# Java uses this, and some people who want to be less verbose than `--`
> my_tool -help
# Microsoft _had_to be different
> my_tool /?
```
If you don't have help text by this point, there probably isn't any. That's often a sign of a bad tool.

## Getting to know git-bash
This teaches:
* A terminal navigates the file system
* You can list files, change folders, make and remove folders and files
* You can start programs from the terminal

**Note**: copy-paste on git-bash doesn't use `ctrl+c` / `ctrl+v`. Use `ctrl+insert` to copy and `shift-insert` to paste. ctrl+c cancels the currently-running program. On cmd, ctrl+c can do both.

```bash
# a terminal is interactive in a call-and-response kind of way
$ echo the echo command prints back to you whatever you write
the echo command prints back to you whatever you write

# a terminal lets you explore your file system
# pwd = "print working directory". A directory is a folder
$ pwd
/

# / is the root of your filesystem on unix / bash
# see what folders are in the current folder with ls ("list storage")
# change directories with cd ("change directory")
$ cd /e # e: drive on my machine. Starting with a slash means relative to the filesystem root.
$ ls
Books/  Code/   Documents/  Notes/

$ cd Notes # starting without a slash means relative to where we are now
$ pwd
/e/Notes

$ cd .. # .. means the parent directory
$ pwd
/e

$ cd Code
$ ls
project1/   project2/

# mkdir = "make directory"
$ mkdir this_project_has_a_long_name
$ ls
project1/   project2/   this_project_has_a_long_name/

# you can start typing a name and hit 'tab' to have the terminal autocomplete. Try it here
$ cd this_ # and then I hit tab, and it autocompleted
$ pwd
/e/Code/this_project_has_a_long_name

$ cd ..
# rmdir = "remove directory"
$ rmdir this_project_has_a_long_name
$ ls
project1/   project2/

# you can create and write to text files with echo and this special arrow
$ echo file contents > my_file.txt
$ ls
project1/   project2/   my_file.txt

# naively typing the file name in bash won't do anything.
# You can do settings per-file, but I won't touch on that here
$ my_file.txt
bash: my_file.txt: command not found

# print the contents of a file with cat = ("con_cat_enate" apparently. This one isn't as good)
$ cat my_file.txt
file contents

# you can start programs from the command-line, with extra parameters to tell them what to open
$ notepad my_file.txt
# This should open notepad, with your file contents on proud display. The shell will block until notepad is closed.
# You can end a line with '&' to make bash not block. You will probably never use this knowledge.

# rm = "remove"
$ rm my_file.txt

# The 'which' command will tell you the location of the thing that would run (if such a tool exists)
$ which git
/mingw64/bin/git

# you can already run git at this point
$ git
usage: git [-v | --version] [-h | --help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           [--config-env=<name>=<envvar>] <command> [<args>]

These are common Git commands used in various situations:
<lots of usage help text>

# A good principle when learning a new command-line tool is to try '<tool> --help', or '<tool> -h' to get it to tell you how to use it
# This isn't useful here as git already did that for us; but it's a good principle to know
$ git --help
<same help text as above>
```

## Getting to know command-prompt (cmd)
Windows cmd is kind of worse than bash in most ways, but it comes with windows so it's what we have. This tutorial will parallel the bash one above one-for-one, so it will be a little more sparse on comments. Text starting with `#` until end-of-line are my comments, don't type that or cmd will get confused. Lines starting with `>` are input by the user, other lines are output by the terminal.
```bash
> echo echo works the same in both terminals, in most ways
echo works the same in both terminals, in most ways

# Print the current directory
> cd
C:\Users\Matthew

# return to drive root
> cd /
> cd
C:\

# Changing drive has a completely different syntax for some reason?
> e:
> cd
E:\

# bash 'ls' = Windows 'dir'
> dir
 Volume in drive E is Data
 Volume Serial Number is <numbers>

 Directory of E:\

2023-08-26  12:01    <DIR>          Books
2023-10-03  21:24    <DIR>          Code
2023-07-01  09:30    <DIR>          Documents
2023-10-03  21:00    <DIR>          Notes
<extra garbage down here>

> cd Notes
> cd
E:\Notes

# .. still means parent directory, just like bash
> cd ..
> cd
E:\

> cd code
# This /B is a 'switch' to make it spew less text at me
> dir /B
project1
project2

# mkdir = "make directory"
> mkdir this_project_has_a_long_name
> dir /B
project1
project2
this_project_has_a_long_name

# in cmd, hitting tab autocompletes directory names (but not git commands :,( )
> cd this_ # I hit tab here and it autocompletes
> cd
E:\Code\this_project_has_a_long_name

> cd ..
# rmdir = "remove directory"
> rmdir this_project_has_a_long_name
> dir /B
project1
project2

# echoing to a file with `>` works the same
> echo my cool file contents > my_file.txt

# You can open the file in notepad the same as bash
> notepad.exe my_file.txt
# opens notepad with the contents of our file. Unlike bash, the terminal is not blocked.

# typing my_file.txt naively will open it with your default text editor / default handler of .txt files
> my_file.txt
# in my case, this opens in notepad++

# some things work the same as bash with a different name:
# bash `cat` = cmd `type`
> type my_file.txt
my cool file contents

# bash `rm` = cmd `del`
> del my_file.txt

# bash `which` = cmd `where`, though where will print backups if it can find multiple things of that name
# if you run the command, the first returned item is what will run
> where git
C:\Program Files\Git\cmd\git.exe

# Running `git` and `git --help` is the same as bash
```
