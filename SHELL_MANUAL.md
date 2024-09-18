# Historical context
A short history of command line interpreters.

1971: Ken Thompson writes the first shell in history, the Thompson Shell, obviously
missing a good chunk of functionalities present in modern shells, such as scripting,
it is nonetheless the precursor for  more accessible and ergonomical file manipulation and command
execution. The name "shell" comes from the fact that it "wraps around" an OS's kernel
both as a safety and usability measure.

1973: Dennis Ritchie creates the C programming language at the AT&T labs. By inspiring the syntax and the functionality of its successors, it is now considered the basis for almost every programming language widely used today, including Shell scripting.

1977: Conception of the original Bourne shell, named after its creator Stephen Bourne. It is the implementation of the shell that brought much of the functionalities we know shell for today, such as pipes `|`, but most importantly scripting with control structures.

1980-90: Usage of DOS/MS-DOS (Microsoft Disk Operating System), Microsoft's first operating system, and one only usable without a graphical interface, and with a command line interface.
It is still present on the latest windows versions, only in the form of the `cmd` application.

1989: Creation of BASH, the Bourne-Again Shell, by Brian Fox and the GNU project. It is without a doubt the most widely used shell today.
> [!NOTE]
> Since the Ubuntu 6.10 linux distribution, the shebang in said distribution written in the following form "**#!/bin/sh**", appears to not direct towards the default BASH as an interpreter but instead uses DASH (Debian Almquist Shell), most likely a performance-related measure. This may cause interpreting problems on non-Debian distributions, hence why it is recommended to specify "**#!/bin/bash**".

2004: First public presentation of MONAD (named after the book Monadology) a .NET framework based shell considered by its creators and users alike to be the prototype for POWERSHELL. The project's chief architect, Jeffrey Snover, meant it as a way to make linux tools available on a Windows system.[^1]
[^1] We can notice part of this design philosophy with some default command aliases that come pre-assigned when installing the latest version of POWERSHELL, which make some commands almost identical to their unix counterpart.

2006: Release of POWERSHELL 1.0 on Windows vista, XP, and server 2003. The latest version of powershell is POWERSHELL 5.0, and comes with most feature we expect from a modern CLI.

# BASH

## COMMAND LINE INTERPRETER
Commands and essential syntax that are a must-know for any beginner programmer in almost any compiled language, or otherwise to consistently naviguate and modify a filesystem.

### Syntax
- **`command`** `-flag 1` `-flag 2` `-flag n` *`argument 1`* *`argument 2`* *`argument n`* = The proper syntax for command execution. In short, the command instructs ***what*** to do, flags define ***how*** the action will be done, and the arguments dictate ***what*** will be affected by the command. Some command however don't require arguments.

- `.` = Signifies the current directory in which you are situated.

- `..` = Signifies the parent directory (Directory above the current one).

- `~` = Signifies the user's home directory. It's defined as a directory containing a user's personal files .

- `/` = Delimiter for specifing directories. The *slash* is typical of unix systems (linux, solaris, slackware...).

> [!IMPORTANT]
> To best understand the following syntax symbols, you need to know the different standard streams of information in UNIX systems. In short, when executing a command, function, or program, data can go in three different directions:
> - Standard Input; abbreviated *STDIN*, and symbolized by a 0, is the stream where the computer takes its information *from*. The most common example of this is a keyboard, where a user types keys.
> - Standard Output; abbreviated *STDOUT*, and symbolized by a 1, is the location where the computer takes its processed information *to*. Following the same example would make our *STDOUT* a screen, where the previously typed keys now appear as formatted UTF-8 characters.
> - Standard Error; abbreviated *STDERR*, and symbolized by a 2, is the channel to which the computer writes its error messages or bug reports should the processing of the input fail, or the input be invalid. It is often quite close to *STDOUT*, because it is useful for the user to know there is an error. That is what happens when you try to name a file or folder with a `/` in it, you will receive a small message warning you that this character is invalid as a name.

- *`cmd1`* **`|`** *`cmd2`*= Pipe, allows for joined simultaneous execution of multiple commands, more accurately, making *cmd1*'s output be *cmd2*'s input. Some commands however don't "get along" when used with the pipe, therefore make sure you use commands that are relevant to eachother's functionalities and outputs.

- *`cmd`* **`>`** *`file`* = Output redirection, while the default output stream is the terminal (displaying output as formatted characters), it is also possible to redirect it to a file. In other words, you can change where *STDOUT* leads to. 

- *`cmd`* **`<`** *`file`* = Input redirection instead of taking its input from the user, it will take it directly from a file.

- *`cmd`* **`>>`** *`file`* = Because output redirection overwrites any pre-existing data in a file, adding two consecutive comparison signs will append the output instead of outright replacing it.

- *`cmd`* **`<<`** *`"delimiter"`* = Proper syntax to start a *heredoc*, it's a type of file that allows for execution of a command with multiple inputs with the condition of ending its execution when a delimiter is met, in other words, the *heredoc* executes `cmd` until `"delimiter"` is met in the file.[^2]
[^2] The most frequent delimiter is the EOF, i.e the End Of File. It's a signal to tell the computer that no more data can be read from the source (in our case, the file).

- *`cmd`* **`2>`** *`file`* = Error redirection, it allows to change the location to which the usual error message caused by a bug. The error will of course still be present, it is merely the message informing the user of the error that will be printed somewhere else.

- `command` `>` `/dev/null` = Syntax to discard the output, indeed sometimes we are not interested in the output of a command, it is in these cases that we may need the directory */dev/null/*, with *null* being a channel that completely removes any trace of data directed to it along with the data itself. It is often used with the syntax `2>&1`, which first directs *STDERR* to *STDOUT* and then *STDOUT* to *null*

### Commands
- **`clear`** = Clears the terminal of all its formatted output.

- **`pwd`** = Prints the current directory (in which you are situated).

- **`cd`** *`/directory/`* = Changes the directory, takes the directory as argument.

- **`ls`** *`/directory/`* or *`file`* = Lists files in the current or specified directory. You can specify a filename present in the current as a first argument, although doing it without flags is not very useful. It is most commonly used with `-l`.

- **`cat`** *`file`* = Concatenates, i.e displays the contents of any text-featuring file. It is most commonly used with `-e`.

- **`less`** *`file`* = Similarly to `cat`, it displays the contents of a file in a tab you can navigate from your command line with specified controls.

- **`grep`** *`pattern`* = When used jointly with a command that displays any sort of formatted output, selectivly displays only those featuring the terms specified as first argument. Most commonly preceded with `|`.

## SCRIPTING
> [!NOTE]
> The following part is dedicated to Shell as a scripting language. Indeed, despite merely consisting of a series of commands executing one after the other, this use of shell (in our case, **BASH**) is considered a proper language, of a higher level than C nonetheless.

### General syntactic conventions
Syntax, proper usage of functionalities and mandatory structures specific to shell as a scripting language.

- .sh = Proper extension of a shell script. Should be executed in your command line like this: `./test.sh`. It is indeed interpreted and not compiled, hence why it is often called a script.

- **#!/bin/sh** = Proper syntax for the **shebang construct** (directory to the proper shell interpreter), this directory is present by default on unix systems. You may in some capacity see it as the Shell equivalent for the C `#include <lib.h>`, only instead of directing towards a standard library of functions (`<lib.h>`), it directs towards the interpreter. May need additional specifications about what shell is used since Ubuntu 6.10 (*See note above ↑*).

- **#** = Signifies a comment. At first, you may find them most useful to "comment out" portions of code you don't need, but you will ultimately not find any better use for them than to leave notes for yourself and other potential contributors because that is their primary function. Indeed, programmers are quite forgetful, and it is crucial that you make the most algorithmically challenging sections of your code, the most well and intelligibly described ones.

- **VAR_NAME=var_contents** = Syntax to initialize a variable, note that the data type is assumed automatically from what the variable contains. (A=1 stores an `integer`, B="hello" stores a `string`...). It is no obligation, but by convention variable names should be in uppercase.

- **$VAR_NAME** = Syntax to access a variable, and therefore its value. Note that the dollar sign (which is the default prompt for bash) is used for accessing, and using it to assign a value to a variable will result in syntax errors.

- **$0 $1 $2 $n** = Respective syntax for the access to arguments specified when running your script in your command line. $0 is logically the name of the script being run, and $1 is the argument after the script. `./your_shell_script.sh` `"argument 1"`,
note that arguments are by default separated by whitespaces[^3], therefore to include arguments with spaces in their file name, you should use double quotations.
[^3] Spaces, tabs, newlines and other "invisible characters", particularly those having a decimal value from 9 to 13, as well as 32, on the ASCII table.

- **$#** = Stores the number of arguments supplied to the scripts. You may view it as the shell equivalent of the C "`int argc`" parameter.

- **$*** = An array (a.k.a, an array) that stores all arguments supplied in the command line when running the script (exept the script filename). You can therefore access it like you would any other array.

- **$?** = The exit status of the last executed command, a (sort of) boolean value that changes depending on the success of said command. Oddly enough, 1 signifies failure, while 0 means success[^4].
[^4] Traditionally, the `boolean` data type is used for expressions with only two possible cases, true representing a 1, or false representing a 0.

- **$$** = Stores the PID, i.e, a unique identification number for the currently open terminal (Process IDentification).

- **$!** = Stores the ID number of the last background command.

- **'str'** or **"str"** = Delimiters used to tell when a string begins, and when it ends. Both single and double quotation can be used to delimit a string in shell.

- `**expr** *operations*`` = Backticks are used to output arithmetic operations in conjunction with the **expr** keyword.

- **[** *$variable1* **==** *$variable2* **]** = Proper syntax for conditions in all control structures (if, elif, else...) used in shell. It notably uses the `long int` type.

- **TABLE[_INDEX_]** = Proper syntax for initializing array variables. Indeed, arrays are considered a type of variable in shell, different than a scalar variable, i.e a single-value variable. Take into account that just like in C, the index starts at 0, which is often confusing for beginners.

- **${TABLE[_INDEX_]}** = Proper syntax for accessing tables. In addition to the typical prompt ($), you also need to add curly brackets.

- **function_identifier(){**
      *function_body*
    **}**
= The proper way to declare a function. Shell functions have a nearly identical functionality to their C counterparts. They therefore excel at dividing code into smaller sections, and avoiding repetition. Though keep in mind that unlike in C, parameters are not initialized inside the parenthesis and are instead specified during a call (**`function_identifier`** *`param1`* *`param2`* ... *`param n`*) and they are accessed in the function body with the prompt followed by the index ($1 $2 ... $n).

### Commands and structures

- **`read`** *`var_name`* = Assigns the user input to a new or pre-declared *variable name*.

- **`unset`** *`var_name`* = Rids a variable of its value.

- **`readonly`** *`var_name`* = Makes a variable "read only" (equivalent to the C "const" keyword). It therfor becomes unsable to take any new assignement.

- **`echo`** *`"str"`* = Prints the string specified as first argument to the command line as formatted output. 

# POWERSHELL

## COMMAND LINE INTERPRETER
The base syntax of powershell couldn't be more different from bash and other unix-like shells and terminals, even sporting a unique name for its commands, `cmdlets` (meaning commandlets, very adorable), however i find the one to one ressemblence of default aliases for some of these commands and basic BASH commands to be a proof of at least some degree of inspiration from BASH, including the presence of a `man` command. Arguments for `cmdlets` are often to be preceded by an informative option-like `parameter`, but it can *sometimes* be ignored. 

### Syntax
> [!IMPORTANT]
> POWERSHELL having parameter-based arguments virually doubles the number of "options" for each command. Therefore, only the most common/useful parameters will be specified, i apologize in advance for the lack of exhaustiveness.
- **`Command-Name.OptionFunc`** `-Parameter 1` *`argument 1`* `-Parameter 2` *`argument 2`* `-Parameter n` *`argument n`* = The proper syntax for command execution and argument specification. The `-Parameter 1` can *sometimes* be omitted, then, the argument simply has to be put in the order the parameter would precede it if it were there. Some commands accept specialized functions accessed like the C direct acces operator (`.`) which allow to shape the output in a specific way, it can therefore be considered the equivalent for BASH options, i.e, ***how*** a command behaves.

- `.` = Signifies the current directory in which you are situated.

- `..` = Signifies the parent directory (Directory above the current one).

- `~` = Signifies the user's home directory in accordance of course with the windows filesystem

- `\` = Delimiter for specifing directories. The *backslash* is typical of Windows systems.

### Commands

- **`New-Item`** *`-Path`* *`path_arg`* *`-ItemType`* *`type_arg`* =  The multipurpose filesystem element creator command in all its glory. Place the absolute or realtive path in which you want to create the file or folder (including the name of said file!) and the file type (Arguments `File`, `Directory`, `SymbolicLink`, `Junction`, `HardLink`) Parameters can be omitted(`New-Item newfile`). Doesn't have default aliases.

- **`Copy-Item`** *`-Path`* *`path_arg`* *`-Destination`* *`dest_arg`* = Self explanatory item copying function. Parameters can be omitted(`Copy-Item src dest`). It has the default aliases `cp` and `copy`.

<!-- WIP -->

<!-- - **`Remove-Item`** *`-Path`* *`path_arg`* -->

<!-- - `Rename-Item` -->

<!-- - `Rename-Item` -->

<!-- - `Get-Content` -->

<!-- - `Invoke-Item` -->

<!-- - Get-ChildItem -->