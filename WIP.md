# THE SHELL
## Historical context
1971. Ken Thompson writes the first shell in history, the Thompson Shell, obviously
missing a good chunk of functionalities present in modern shells, such as scripting,
it is nonetheless precursor for accessible ergonomical file manipulation and command
execution. The name shell comes from the fact that it "wraps around" an OS's kernel
both as a safety and usability measure.

1973. Dennis Ritchie creates the C programming language at the AT&T labs, it's the basis for almost every programming language today.

~1977. Conception of the original Bourne shell, named after its creator stephen bourne 
## Essential commands and syntax
Commands and essential syntax that are a must-know for any beginner programmer in almost any compiled language, or otherwise to consistently naviguate and modify a filesystem. Here i won't detail all of the flags, as you can easily look up a manual page for detailed information of each command (**`man`** *`command_name`*). I will however feature the most commonly used flags.

### Syntax
- **`command`** `-flag 1` `-flag 2` `-flag n` *`argument 1`* *`argument 2`* *`argument n`* = The proper syntax for command execution. In short, the command instructs ***what*** to do, flags define ***how*** the action will be done, and the arguments dictate ***what*** will be affected by the command. Some command however don't require arguments.

- `.` = Defines the current directory.

- `..` = Defines the parent directory (Directory above the current one).

- `~` = Defines the user's home directory. It's defined as a directory containing a user's personal files .

- `\` or `/` = Delimiter for specifing directories. The first one (*backslash*) is typical of unix systems (linux), while the latter (*slash*) is the norm on windows systems.

### Commands
- **`clear`** = Clears the terminal of all its formatted output.

- **`pwd`** = Print working directory.

- **`cd`** *`directory/`* = Change directory, takes the directory as argument.

- **`ls`** = List files in current or specified directory. Most commonly used with `-l`.

- **`cat`** = Concatenate, displays the contents of any text featuring file. Most commonly used with `-e`.

- **`less`** = Similarly to cat, displays contents of a file in a tab you can naviguate from your command line with specified commands.

- **`grep`** *`pattern`* = when used jointly with a command that displays any sort of formatted output, selectivly displays only those featuring the word specified as first argument. Most commonly preceded with `|`.

- **`find`** *`pattern`*

# SHELL PROGRAMMING
## General syntactic conventions
- **`HASHTAG`** = Signifies a comment. 

- #!/bin/sh = proper syntax for the **shebang construct** (directory to the proper shell interpreter),this directory is present by default on unix systems.

- **`read`** *`var_name`* = assigns the user input to a new *variable name*

- **`unset`** *`var_name`* = unsets a variable

- **`readonly`** *`var_name`* = makes a variable "read only" (equivalent to the C "const" keyword)

- **`echo`** *`"str"`* = Is indeed a command, that prints the strings specified as first argument 

- **'str'** or **"str"** = both single and double quotation can be used to delimit a string in shell

- **`expr`** operations= backticks are used to output arithmetic operations in conjunction with the **expr** keyword

- **[** *$variable1* **==** *$variable2* **]** = General syntax for conditions in all control structures (if, elif, else...) used in shell. It notably uses the `long int` type.
