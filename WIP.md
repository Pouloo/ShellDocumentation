# THE SHELL
## Historical context
1971. Ken Thompson writes the first shell in history, the Thompson Shell, obviously
missing a good chunk of functionalities present in modern shells, such as scripting,
it is nonetheless precursor for accessible ergonomical file manipulation and command
execution. The name shell comes from the fact that it "wraps around" an OS's kernel
both as a safety and usability measure.

1973. Dennis Ritchie creates the C programming language at the AT&T labs, it's the basis for almost every programming language today.

~1977. Conception of the original Bourne shell, named after its creator stephen bourne 
## ESSENTIAL COMMANDS
> [!NOTE]
> Commands that are a must-know for any beginner programmer in almost any compiled language, or otherwise to consistently naviguate and modify a filesystem. Here i won't detail all of the flags, as you can easily look up a manual page for detailed information of each command (**`man`** *`command_name`*). I will however feature the most commonly used ones.

- **`pwd`**

- `cd `

- `ls`


# SHELL PROGRAMMING
## General syntactic conventions
- **hashtag** = comment (ascii symbol not used because of github formating)

- !/bin/sh = proper syntax for the **shebang construct** (directory to the proper shell interpreter),this directory is present by default on unix systems.

- **read** *var_name* = assigns the user input to a new *variable name*

- **unset** *var_name* = unsets a variable

- **readonly** *var_name* = makes a variable "read only" (equivalent to the C "const" keyword)

- **echo** *str* = 

- **'_str_'** or **"_str_"** = both single and double quotation can be used to delimit a string in shell

- **`expr _operations_`** = backticks are used to output arithmetic operations in conjunction with the **expr** keyword

- **[ _$variable1_ == _$variable2_ ]** = proper syntax for assignement operation (uses long int)
