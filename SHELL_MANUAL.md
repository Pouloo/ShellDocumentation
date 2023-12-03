# THE SHELL
## Historical context
A short history of command line interpreters.

1971: Ken Thompson writes the first shell in history, the Thompson Shell, obviously
missing a good chunk of functionalities present in modern shells, such as scripting,
it is nonetheless precursor for accessible ergonomical file manipulation and command
execution. The name shell comes from the fact that it "wraps around" an OS's kernel
both as a safety and usability measure.

1973: Dennis Ritchie creates the C programming language at the AT&T labs. By inspiring the syntax and the functionality of its successors, it is now considered the basis for almost every programming language widely used today, including Shell scripting.

1977: Conception of the original Bourne shell, named after its creator Stephen Bourne. It is the implementation of the shell that brought much of the functionalities we know shell for today, such as pipes `|`, but most importantly scripting with control structures.

1989: Creation of BASH, the Bourne-Again Shell, by Brian Fox and the GNU project. Most widely used shell today.
> [!NOTE]
> Since Ubuntu 6.10, the shebang in the following form "**#!/bin/sh**", appears to not direct towards the default BASH as an interpreter but instead uses DASH (Debian Almquist Shell), most likely a performance-related measure. This may cause interpreting problems on non-Debian distributions, hence why it is recommended to specify "**#!/bin/bash**".

## Essential commands and syntax
Commands and essential syntax that are a must-know for any beginner programmer in almost any compiled language, or otherwise to consistently naviguate and modify a filesystem.

### Syntax
- **`command`** `-flag 1` `-flag 2` `-flag n` *`argument 1`* *`argument 2`* *`argument n`* = The proper syntax for command execution. In short, the command instructs ***what*** to do, flags define ***how*** the action will be done, and the arguments dictate ***what*** will be affected by the command. Some command however don't require arguments.

- `.` = Defines the current directory.

- `..` = Defines the parent directory (Directory above the current one).

- `~` = Defines the user's home directory. It's defined as a directory containing a user's personal files .

- `/` or `\` = Delimiter for specifing directories. The first one (*slash*) is typical of unix systems (linux), while the latter (*backslash*) is the norm on windows systems.

- `|` = pipe

### Commands
- **`clear`** = Clears the terminal of all its formatted output.

- **`pwd`** = Print working directory.

- **`cd`** *`/directory/`* = Change directory, takes the directory as argument.

- **`ls`** = List files in current or specified directory. Most commonly used with `-l`.

- **`cat`** = Concatenate, displays the contents of any text featuring file. Most commonly used with `-e`.

- **`less`** = Similarly to cat, displays contents of a file in a tab you can naviguate from your command line with specified commands.

- **`grep`** *`pattern`* = when used jointly with a command that displays any sort of formatted output, selectivly displays only those featuring the word specified as first argument. Most commonly preceded with `|`.

# SHELL PROGRAMMING
> [!NOTE]
> The following part is dedicated to Shell as a scripting language. Indeed, despite merely consisting of a series of commands executing on after the other, this use of shell (In our case **BASH**) is considered a proper language, of a higher level than C nonetheless.

## General syntactic conventions
Syntax, proper usage of functionalities and mandatory structures specific to shell as a scripting language.

- .sh = Proper extension of a shell script. Should be executed in your command line like this: `./test.sh`. It is indeed interpreted and not compiled, hence why it is called a script, and not a program.

- **#!/bin/sh** = Proper syntax for the **shebang construct** (directory to the proper shell interpreter), this directory is present by default on unix systems. May need additional specifications about what shell is used since Ubuntu 6.10 (*See note above ↑*)

- **#** = Signifies a comment.

- **VAR_NAME=var_contents** = Syntax for variable initialization, note that the data type is assumed automatically from what the variable contains. (A=1 stores an `int`, B="hello" stores a `string`...). It is no obligation, but by convention variable names should be in uppercase.

- **$VAR_NAME** = Variable access, the dollar sign is the default prompt for bash.

- **$0 $1 $2 $n** = Respective access to arguments specified to your script. $0 is logically the name of the script being run.

- **$#** = Stores the number of arguments supplied to the scripts. You may view it as the shell equivalent of the C "`int argc`" parameter.

- **$*** = Stores all arguments supplied in the command line.

- **$?** = The exit status of the last executed command, a (sort of) boolean value changing depending on the sucess of said command. Oddly enough, 1 signifies failure, while 0 means sucess.

- **$$** = Stores the PID, identification number of the current Shell.

- **$!** = Stores the id number of the last background command.

- **'str'** or **"str"** = Both single and double quotation can be used to delimit a string in shell.

- `**expr** *operations*`` = Backticks are used to output arithmetic operations in conjunction with the **expr** keyword.

- **[** *$variable1* **==** *$variable2* **]** = General syntax for conditions in all control structures (if, elif, else...) used in shell. It notably uses the `long int` type.

## Commands and structures

- **`read`** *`var_name`* = Assigns the user input to a new or pre-declared *variable name*.

- **`unset`** *`var_name`* = Rids a variable of its value.

- **`readonly`** *`var_name`* = Makes a variable "read only" (equivalent to the C "const" keyword). It therfor becomes unsable to take any new assignement.

- **`echo`** *`"str"`* = Prints the string specified as first argument to the command line as formatted output. 
