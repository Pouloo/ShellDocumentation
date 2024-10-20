# Historical context

A short history of command line interpreters.

1971: Ken Thompson writes the first shell in history, the Thompson Shell, obviously
missing a good chunk of functionalities present in modern shells, such as scripting,
it is nonetheless the precursor for more accessible and ergonomical file manipulation and command execution. The name "shell" comes from the fact that it "wraps around" an OS's kernel
both as a safety and usability measure.

1973: Dennis Ritchie creates the C programming language at the AT&T labs. By inspiring the syntax and the functionality of its successors, it is now considered the basis for almost every programming and scripting language widely used today, including Shell scripting.

1977: Conception of the original Bourne shell, named after its creator Stephen Bourne. It is the implementation of the shell that brought much of the functionalities we know shell for today, such as pipes `|`, but most importantly scripting with control structures (if, else...).

1980-90: Usage of DOS/MS-DOS (Microsoft Disk Operating System), Microsoft's first operating system, and one only usable without a graphical interface, and with a command line interface. It is still present on the latest windows versions, only in the form of the `cmd` application.

1989: Creation of BASH, the Bourne-Again Shell, by Brian Fox and the GNU project. With It is without a doubt the most widely used shell today.

2004: First public presentation of MONAD (named after the book Monadology) a .NET framework based shell considered by its creators and users alike to be the prototype for POWERSHELL. The project's chief architect, Jeffrey Snover, meant it as a way to make linux tools available on a Windows system.[^1]
[^1] We can notice part of this design philosophy with some default command aliases that come pre-assigned when installing the latest version of POWERSHELL, which make some commands almost identical to their UNIX counterpart.

2006: Release of POWERSHELL 1.0 on Windows vista, XP, and server 2003. The latest version of powershell is POWERSHELL 5.0, and comes with most feature we expect from a modern CLI.
> [!NOTE]
> Since the Ubuntu 6.10 linux distribution, the shebang in said distribution written in the following form "**#!/bin/sh**", appears to not direct towards the default BASH as an interpreter but instead uses DASH (Debian Almquist Shell), most likely a performance-related measure. This may cause interpreting problems on non-Debian distributions, hence why it is recommended to specify "**#!/bin/bash**".

# BASH

## COMMAND LINE INTERPRETER

Commands and essential syntax that are a must-know for any beginner programmer in almost any compiled language, or otherwise to consistently naviguate and modify a filesystem.

### Syntax

- **`command`** `-flag 1` `-flag 2` `-flag n` *`argument 1`* *`argument 2`* *`argument n`* = The proper syntax for command execution. In short, the command instructs ***what*** to do, flags define ***how*** the action will be done, and the arguments dictate ***what*** will be affected by the command. Some command however don't require arguments.

> [!IMPORTANT]
> To best understand the following syntax symbols, you need to know the different standard streams of information in UNIX systems. In short, when executing a command, function, or program, data can go in three different directions:
> - Standard Input; abbreviated *STDIN*, and symbolized by a 0, is the stream where the computer takes its information *from*. The most common example of this is a keyboard, where a user types keys.
> - Standard Output; abbreviated *STDOUT*, and symbolized by a 1, is the location where the computer takes its processed information *to*. Following the same example would make our *STDOUT* a screen, where the previously typed keys now appear as formatted UTF-8 characters.
> - Standard Error; abbreviated *STDERR*, and symbolized by a 2, is the channel to which the computer writes its error messages or bug reports should the processing of the input fail, or the input be invalid. It is often quite close to *STDOUT*, because it is useful for the user to know there is an error. That is what happens when you try to name a file or folder with a `/` in it, you will receive a small message warning you that this character is invalid as a name.

- `.` = Signifies the current directory in which you are situated.

- `..` = Signifies the parent directory (Directory above the current one).

- `~` = Signifies the user's home directory. It's defined as a directory containing a user's personal files .

- `/` = Delimiter for specifing directories. The *slash* is typical of UNIX systems (linux, solaris, slackware...).

- *`cmd1`* **`|`** *`cmd2`*= Pipe, allows for joined simultaneous execution of multiple commands, more accurately, making *cmd1*'s output be *cmd2*'s input. Some commands however don't "get along" when used with the pipe, therefore make sure you use commands that are relevant to eachother's functionalities and outputs. The workings of the pipe align well with the UNIX philosophy principle of *"One function's output should be another's input"*, and are technically more complexe than this short manual can describe.

- *`cmd`* **`>`** *`file`* = Output redirection, while the default output stream is the terminal (displaying output as formatted characters), it is also possible to redirect it to a file. In other words, you can change where *STDOUT* leads to. 

- *`cmd`* **`<`** *`file`* = Input redirection instead of taking its input from the user, it will take it directly from a file.

- *`cmd`* **`>>`** *`file`* = Because output redirection overwrites any pre-existing data in a file, adding two consecutive comparison signs will append the output instead of outright replacing it.

- *`cmd`* **`<<`** *`"delimiter"`* = Proper syntax to start a *heredoc*, it's a type of file that allows for execution of a command with multiple inputs with the condition of ending its execution when a delimiter is met, in other words, the *heredoc* executes `cmd` until `"delimiter"` is met in the file.[^2]
[^2] The most frequent delimiter is the EOF, i.e the End Of File. It's a signal to tell the computer that no more data can be read from the source (in our case, the file).

- *`cmd`* **`2>`** *`file`* = Error redirection, it allows to change the location to which the usual error message caused by a bug. The error will of course still be present, it is merely the message informing the user of the error that will be printed somewhere else.

- `command` `>` `/dev/null` = Syntax to discard the output, indeed sometimes we are not interested in the output of a command, it is in these cases that we may need the directory */dev/null/*, with *null* being a channel that completely removes any trace of data directed to it along with the data itself. It is often used with the syntax `2>&1`, which first directs *STDERR* to *STDOUT* and then *STDOUT* to *null*

<!-- - *`'/n'`* = escape sequence -->

### Commands (basic)

- **`clear`** = Clears the terminal of all its formatted output.

- **`pwd`** = Prints the current directory (in which you are situated) in the classic UNIX directory delimiting (`/`). Takes no parameters.

- **`cd`** *`/directory/`* = Changes the directory, takes the directory as argument.

- **`ls`** *`/directory/`* or *`file`* = Lists files in the current or specified directory. You can specify a filename present in the current as a first argument, although doing it without flags is not very useful. It is most commonly used with `-l`.

- **`cat`** *`file`* = Concatenates, i.e displays the contents of any text-featuring file. The default content, and the one we want *most of the time* is the raw text data, and in that regard, it possesses a mostly output formatting flags (`-e` shows the end of line (EOF), others display whitespaces as control characters...), and becomes particularly useful when used in tandem with output redirection (with which `cat` can write to a file with `>` or even append with `>>`).

- **`rm`** *`file_or_directory_1`* *`file_or_directory_2`* *`file_or_directory_n`* = The all powerful **permanent** file removal tool. Use with `-r` to remove directories and their files, `-i` when you need to opt on the side of caution (prompt before each removal) and use `-f` at your own risk (never prompt and ignore special cases, except administrative privilege requirements)

- **`less`** *`file`* = Similarly to `cat`, it displays the contents of a file in a tab you can navigate from your command line with specified controls.

- **`more`** *`file`* = 

- **`grep`** *`pattern`* = When used jointly with a command that displays any sort of formatted output, selectivly displays only those matching patterns of words specified as first argument. Must be preceded with `|`.

<!-- - **`pushd`** ; **`popd`** ; **`dirs`** = These three commands go hand in hand, hence why i specified them together-->

<!-- - **`wc`** = Content counter, said content can be anything between the number of characters, -->

### Commands (advanced)

- **`alias`** *`identifier="cmd1; cmd2; cmdn"`* = Set alias, it can be anything from a series of in-order executed commands to script functions, all called by a user defined `identifier`, allowing for simplicity and egonomics within the comfort of the terminal.

<!-- - **`sed`** -->

<!-- - **`awk`** -->

<!-- - **`ifconfig`** -->

<!-- - **`source`** -->

<!-- **`export`** -->

<!-- - **`git`** -->

## SCRIPTING

> [!NOTE]
> The following part is dedicated to Shell as a scripting language. Indeed, despite merely consisting of a series of commands executing one after the other, this use of shell (in our case, **BASH**) is considered a proper language, of a higher level than C nonetheless.

### Syntax and variables

Syntax, proper usage of functionalities and mandatory structures specific to shell as a scripting language.

- .sh = Proper extension of a shell script. Should be executed in your command line like this: `./test.sh`. It is indeed interpreted and not compiled, hence why it is often called a script.

- **`#!/bin/sh`** = Proper syntax for the **shebang construct** (directory to the proper shell interpreter), this directory is present by default on UNIX systems. You may in some capacity see it as the Shell equivalent for the C `#include <lib.h>`, only instead of directing towards a standard library of functions (`<lib.h>`), it directs towards the interpreter. May need additional specifications about what shell is used since Ubuntu 6.10 (*See note above ↑*).

- **`#`** = Signifies a comment. At first, you may find them most useful to "comment out" portions of code you don't need, but you will ultimately not find any better use for them than to leave notes for yourself and other potential contributors because that is their primary function. Indeed, programmers are quite forgetful, and it is crucial that you make the most algorithmically challenging sections of your code, the most well and intelligibly described ones.

- **`VAR_NAME=var_contents`** = Syntax to initialize a variable, note that the data type is assumed automatically from what the variable contains. (A=1 stores an `integer`, B="hello" stores a `string`...). It is no obligation, but by convention variable names should be in uppercase.

- **`$VAR_NAME`** = Syntax to access a variable, and therefore its value. Note that the dollar sign (which is the default prompt for bash) is used for accessing, and using it to assign a value to a variable will result in syntax errors.

- **`$0 $1 $2 $n`** = Respective syntax for the access to arguments specified when running your script in your command line. $0 is logically the name of the script being run, and $1 is the argument after the script. `./your_shell_script.sh` `"argument 1"`, note that arguments are by default separated by whitespaces[^3], therefore to include arguments with spaces in their file name, you should use double quotations. When used inside a function body, they refer to the function's parameters/arguments, and not the program's.
[^3] Spaces, tabs, newlines and other "invisible characters", particularly those having a decimal value from 9 to 13, as well as 32, on the ASCII table.

- **`$#`** = Stores the number of arguments supplied to the scripts. You may view it as the shell equivalent of the C "`int argc`" parameter.

- **`$*`** = An array (a.k.a, an array) that stores all arguments supplied in the command line when running the script (exept the script filename). You can therefore access it like you would any other array.

- **`$?`** = The exit status of the last executed command, a (sort of) boolean value that changes depending on the success of said command. Oddly enough, 1 signifies failure, while 0 means success[^4].
[^4] Traditionally, the `boolean` data type is used for expressions with only two possible cases, true representing a 1, or false representing a 0.

- **`$$`** = Stores the PID, i.e, a unique identification number for the currently open terminal (Process IDentification).

- **`$!`** = Stores the ID number of the last background command.

- **`'str'`** or **`"str"`** = Delimiters used to tell when a string begins, and when it ends. Both single and double quotation can be used to delimit a string in shell.

- **[** *$variable1* **==** *$variable2* **]** = Proper syntax for conditions in all control structures (if, elif, else...) used in shell. It notably uses the `long int` type.

- **`TABLE[_INDEX_]`** = Proper syntax for initializing array variables. Indeed, arrays are considered a type of variable in shell, different than a scalar variable, i.e a single-value variable. Take into account that just like in C, the index starts at 0, which is often confusing for beginners.

- **`${TABLE[_INDEX_]}`** = Proper syntax for accessing tables. In addition to the typical prompt ($), you also need to add curly brackets.

- **`function_identifier() {function_body}`** = The proper way to declare a function. Shell functions have a nearly identical functionality to their C counterparts. They therefore excel at dividing code into smaller sections, and avoiding repetition. Though keep in mind that unlike in C, parameters are not initialized inside the parenthesis and are instead specified during a call (`function_identifier` `param1` `param2` ... *`param n`) and they are accessed in the function body with the prompt followed by the index ($1 $2 ... $n).

### Commands and structures

- **`read`** *`var_name`* = Assigns the user input to a new or pre-declared *variable name*.

- **`unset`** *`var_name`* = Rids a variable of its value.

- **`readonly`** *`var_name`* = Makes a variable "read only" (equivalent to the C "const" keyword). It therfore becomes unsable to take any new assignement.

- **`echo`** *`"str"`* = Prints the string, character or escape sequence (or of course, all at once) specified as first argument to the command line as formatted output. 

- **(BACKTICK)`expr** *operations`(BACKTICK)* = Default command for shell based arithmetic operations. All operations within the backticks (replaced by onomatopoeia because of Markdown[^5] syntax) are considered as arithmetic operations and allow
[^5] Markdown is a 2004 "lightweight markup language" designed for formatting raw text data. Widely implemented today from ChatGPT answers to general documentation, hence the use of the .md (**M**ark**D**own) file extension by github. See https://en.wikipedia.org/wiki/Markdown.

<!-- - **`if [ ] then fi`** -->

<!-- - **`else [ ] fi`** -->

<!-- - **`elif [ ] then fi`** -->

<!-- **`until [ ] do done`** -->

<!-- **`while [ ] do done`** -->

<!-- **`for [ ] do done`** -->

<!-- **`case $VAR in`** -->

<!-- **`select $VAR val1 valn do done`** -->

# POWERSHELL

## COMMAND LINE INTERPRETER

> [!NOTE]
> The base syntax of powershell couldn't be more different from bash and other UNIX-like shells and terminals, even sporting a unique name for its commands, `cmdlets` (meaning commandlets, very adorable), however i find the one to one ressemblence of default aliases for some of these commands and basic BASH commands to be a proof of at least some degree of inspiration from BASH, including the presence of a `man` command. Arguments for `cmdlets` are often to be preceded by an informative option-like `parameter`, but it can *sometimes* be ignored. 

### Syntax

> [!NOTE]
> POWERSHELL having parameter-based arguments virtually doubles the number of "options" for each command. Therefore, only the most common/useful parameters will be specified, i apologize in advance and again for the lack of exhaustiveness.

- **`Command-Name.OptionFunc`** `-Parameter 1` *`argument 1`* `-Parameter 2` *`argument 2`* `-Parameter n` *`argument n`* = The proper syntax for cmdlets execution and argument specification. The `-Parameter 1` can *sometimes* be omitted, then, the argument simply has to be put in the order the parameter would precede it if it were there. Some commands accept specialized functions accessed like with the C direct access operator (`.`) which allow to shape the output in a specific way, it can therefore be considered the equivalent for BASH options, i.e, ***how*** a command behaves.

- `.` = Signifies the current directory in which you are situated.

- `..` = Signifies the parent directory (Directory above the current one).

- `~` = Signifies the user's home directory in accordance of course with the windows filesystem

- `\` = Delimiter for specifing directories. The *backslash* is typical of Windows systems.

### Commands (basic)

- **`Get-Location`** = Non argumented (taking no argument) cmdlet displaying the current directory (in which the user is currently situated) in the classic MS-DOS/Windows fashion, with the backslash `\`. Specify the drive in which you want to search the path with `-PSDrive` `drive_letter`

- **`Clear-Content`** `file` = Deletes all content of the file.

- **`New-Item`** *`-Path`* *`path_arg`* *`-ItemType`* *`type_arg`* =  The multipurpose filesystem element creator command in all its glory. Place the absolute or realtive path in which you want to create the file or folder (including the name of said file!) and the file type (Arguments `File`, `Directory`, `SymbolicLink`, `Junction`, `HardLink`) Parameters can be omitted(`New-Item newfile`). Doesn't have default aliases.

- **`Copy-Item`** *`-Path`* *`path_arg`* *`-Destination`* *`dest_arg`* = Self explanatory item copying function. Parameters can be omitted(`Copy-Item src dest`). It has the default aliases `cp` and `copy`.

- **`Set-Content`** *-Path* *`path_arg`* *-Value* *`string`* = Writes and replaces the content of the writable file specified at `-Path`, by the string of characters at `-Value`. If no file with the name at path is present, the file is created.

- **`Add-Content`** *-Path* *`path_arg`* *-Value* *`string`* = Writes the string specified at `-Value` after a newline written after the existing contents of the file at `-Path`.

- **`Get-Content`** = Command used for reading a file's contents, but unlike its BASH equivalent `cat`, the content output can be modulated and include such things as a file's length, a certain number of lines from a file (`-TotalCount`), or reading a "alternate data stream".

- **`Remove-Item`** *`-Path`* *`path_arg`* = Permanently removes files, folders and links (equivelent to pressing the `DEL` key when selecting a file in the file explorer). Contrary to the trivial BASH `rm` options, the `Remove-Item` gives several, command-imbedded (i.e, not relying on wildcards like `*`) parameters for excluding files or filetypes (-Exclude), and only deleting specific file names (-Include), among others.

- **`Move-Item`** *`-Path`* *`path_arg`* = Moves files from a source to a destination, and unlike BASH, can't be used to rename files. Included with the alias `mv`.

- **`Rename-Item`** *-Path* *`path_arg`* *`-NewName`* *`new_name_arg`* = Instead of using the `mv` command to rename entities in your filesystem such as in bash, there is a separate command for that in POWERSHELL, and a separate alias `rni`.

> [!NOTE]
> As you may have noticed, in contrast to the laconic and cryptic bash commands and their plethora of flags, some cmdlets are quite explicit and redundant in their names and functionalities, a trend that seems to endure in most sets of cmdlets. You could say this hyper-ramification (one command does one thing) is again a result of a design philosophy, to make the cmdlets as understandable as possible with a Verb-Noun naming convention.

- **`Sort-Object`** *`-Proprety`* *`object`* = Sorts table of unsorted (obviously) integers or alphanumerical characters in crescent (increasing) order.
 
- **`Get-Culture`** = Displays a few localization settings for your current system, or following a specific name with `-Name`.

- **`Get-History`** *`-Count`* *`last_count_cmdlets`* = Displays the history of the last `count` commands in your currently open terminal session.

### Commands (advanced)

- **`Format-List`** *`-InputObject`* *`data`* = Cmdlet used to format lots of information into an easily understandable list with separate attributes, as well as displaying additional information about the file timestamp, filetype, ecetera. Using it on regular files with few contents is redundand, and it is best utilized with a `|`, and a long output command

- **`Get-Unique`** *`-InputObject`* *`object`* = Only display duplicate values 1 time from a sorted table. Therefore, often used in tandem with the `Sort-Object` command.

- **`Invoke-Item`** *`-Path`* *`item`* = Performs the default action on the specified item. In other words, it emulates a *double-click* on an app, executable or file icon, and therefore opens it with the set default application.

- **`Compare-Object`** *`-ReferenceObject`* *`ref_content_object`* *`-DifferenceObject`* *`diff_content_object`* = POSH equivalent of the BASH `diff` (coincidently accessible through the `diff` alias). Displays the difference between specified **objects** (and these objects DO NOT include a file path, only their contents accessed separatly, for instance with `Get-Content`)

- **`Measure-Object`** *`-Object`* *`object`* = Displays information such as the number of characters, words, and lines of a string object specified as argument (-Character, -Line, -Word). Can be used to measure this data on a file by getting the content from said file.

<!-- - **`Set-Date`** =  -->

<!-- - **`Get-Date`** -->

<!-- - **`Measure-Object`** -->

<!-- - **`Get-ChildItem`** *``* =  -->
