# THE SHELL
## Historical context
A short history of command line shells.

1971: Ken Thompson writes the first shell in history, the Thompson Shell, obviously
missing a good chunk of functionalities present in modern shells, such as scripting,
it is nonetheless precursor for accessible ergonomical file manipulation and command
execution. The name shell comes from the fact that it "wraps around" an OS's kernel
both as a safety and usability measure.

1973: Dennis Ritchie creates the C programming language at the AT&T labs. By inspiring the syntax and the functionality of its successors, it is now considered the basis for almost every programming language widely used today, including Shell scripting.

1977: Conception of the original Bourne shell, named after its creator Stephen Bourne. It is the implementation of the shell that brought much of the functionalities we know shell for today, such as pipes `|`, but most importantly scripting with control structures.

1989: Creation of BASH, the Bourne-Again Shell, by Brian Fox and the GNU project. It is without a doubt the most widely used shell today.
> [!NOTE]
> Since Ubuntu 6.10, the shebang in the following form "**#!/bin/sh**", appears to not direct towards the default BASH as an interpreter but instead uses DASH (Debian Almquist Shell), most likely a performance-related measure. This may cause interpreting problems on non-Debian distributions, hence why it is recommended to specify "**#!/bin/bash**".

## Essential commands and syntax
Commands and essential syntax that are a must-know for any beginner programmer in almost any compiled language, or otherwise to consistently naviguate and modify a filesystem.

### Syntax
- **`command`** `-flag 1` `-flag 2` `-flag n` *`argument 1`* *`argument 2`* *`argument n`* = The proper syntax for command execution. In short, the command instructs ***what*** to do, flags define ***how*** the action will be done, and the arguments dictate ***what*** will be affected by the command. Some command however don't require arguments.

- `.` = Signifies the current directory in which you are situated.

- `..` = Signifies the parent directory (Directory above the current one).

- `~` = Signifies the user's home directory. It's defined as a directory containing a user's personal files .

- `/` or `\` = Delimiter for specifing directories. The first one (*slash*) is typical of unix systems (linux), while the latter (*backslash*) is the norm on windows systems.

- `|` = Pipe, allows for joined simultaneous execution of multiple commands. Some commands however don't "get along" when used with the pipe, therefore make sure you use commands that are relevent to eachother's functionalities and outputs.

### Commands
- **`clear`** = Clears the terminal of all its formatted output.

- **`pwd`** = Prints the current directory (in which you are situated).

- **`cd`** *`/directory/`* = Changes the directory, takes the directory as argument.

- **`ls`** *`/directory/`* or *`file`* = Lists files in the current or specified directory. You can specify a filename present in the current as a first argument, although doing it without flags is not very useful. It is most commonly used with `-l`.

- **`cat`** *`file`* = Concatenates, i.e displays the contents of any text-featuring file. It is most commonly used with `-e`.

- **`less`** *`file`* = Similarly to `cat`, it displays the contents of a file in a tab you can navigate from your command line with specified controls.

- **`grep`** *`pattern`* = When used jointly with a command that displays any sort of formatted output, selectivly displays only those featuring the terms specified as first argument. Most commonly preceded with `|`.

# SHELL PROGRAMMING
> [!NOTE]
> The following part is dedicated to Shell as a scripting language. Indeed, despite merely consisting of a series of commands executing one after the other, this use of shell (in our case, **BASH**) is considered a proper language, of a higher level than C nonetheless.

## General syntactic conventions
Syntax, proper usage of functionalities and mandatory structures specific to shell as a scripting language.

- .sh = Proper extension of a shell script. Should be executed in your command line like this: `./test.sh`. It is indeed interpreted and not compiled, hence why it is often called a script.

- **#!/bin/sh** = Proper syntax for the **shebang construct** (directory to the proper shell interpreter), this directory is present by default on unix systems. You may in some capacity see it as the Shell equivalent for the C `#include <lib.h>`, only instead of directing towards a standard library of functions (`<lib.h>`), it directs towards the interpreter. May need additional specifications about what shell is used since Ubuntu 6.10 (*See note above ↑*).

- **#** = Signifies a comment. At first, you may find them most useful to "comment out" portions of code you don't need, but you will ultimately not find any better use for them than to leave notes for yourself and other potential contributors because that is their primary function. Indeed, programmers are quite forgetful, and it is crucial that you make the most algorithmically challenging sections of your code, the most well and intelligibly described ones.

- **VAR_NAME=var_contents** = Syntax to initialize a variable, note that the data type is assumed automatically from what the variable contains. (A=1 stores an `integer`, B="hello" stores a `string`...). It is no obligation, but by convention variable names should be in uppercase.

- **$VAR_NAME** = Syntax to access a variable, and therefore its value. Note that the dollar sign (which is the default prompt for bash) is used for accessing, and using it to assign a value to a variable will result in syntax errors.

- **$0 $1 $2 $n** = Respective syntax for the access to arguments specified when running your script in your command line. $0 is logically the name of the script being run, and $1 is the argument after the script. `./your_shell_script.sh` `"argument 1"`,
note that arguments are by default separated by whitespaces[^1], therefore to include arguments with spaces in their file name, you should use double quotations.
[^1] Spaces, tabs, newlines and other "invisible characters", particularly those having a decimal value from 9 to 13, as well as 32, on the ASCII table.

- **$#** = Stores the number of arguments supplied to the scripts. You may view it as the shell equivalent of the C "`int argc`" parameter.

- **$*** = An array (a.k.a, an array) that stores all arguments supplied in the command line when running the script (exept the script filename). You can therefore access it like you would any other array.

- **$?** = The exit status of the last executed command, a (sort of) boolean value that changes depending on the success of said command. Oddly enough, 1 signifies failure, while 0 means success[^2].
[^2] Traditionally, the `boolean` data type is used for expressions with only two possible cases, true representing a 1, or false representing a 0.

- **$$** = Stores the PID, i.e, a unique identification number for the currently open terminal (Process IDentification).

- **$!** = Stores the ID number of the last background command.

- **'str'** or **"str"** = Delimiters used to tell when a string begins, and when it ends. Both single and double quotation can be used to delimit a string in shell.

- `**expr** *operations*`` = Backticks are used to output arithmetic operations in conjunction with the **expr** keyword.

- **[** *$variable1* **==** *$variable2* **]** = Proper syntax for conditions in all control structures (if, elif, else...) used in shell. It notably uses the `long int` type.

- **TABLE[_INDEX_]** = Proper syntax for initializing array variables. Indeed, arrays are considered a type of variable in shell, different than a scalar variable, i.e a single-value variable. Take into account that just like in C, the index starts at 0, which is often confusing for beginners.

- **${TABLE[_INDEX_]}** = Proper syntax for accessing tables. In addition to the typical prompt ($), you also need to add curly brackets.

## Commands and structures

- **`read`** *`var_name`* = Assigns the user input to a new or pre-declared *variable name*.

- **`unset`** *`var_name`* = Rids a variable of its value.

- **`readonly`** *`var_name`* = Makes a variable "read only" (equivalent to the C "const" keyword). It therfor becomes unsable to take any new assignement.

- **`echo`** *`"str"`* = Prints the string specified as first argument to the command line as formatted output. 
