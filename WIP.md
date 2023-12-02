# THE SHELL
## Historical context
1971. Ken Thompson writes the first shell in history, the Thompson Shell, obviously
missing a good chunk of functionalities present in modern shells, such as scripting,
it is nonetheless precursor for accessible ergonomical file manipulation and command
execution. The name shell comes from the fact that it "wraps around" an OS's kernel
both as a safety and usability measure.

1973. Dennis Ritchie creates the C programming language at the AT&T labs, it's the basis
for almost every programming language today.


# SHELL PROGRAMMING

- <hashtag> = comment (ascii symbol not used because of github formating)

- #!/bin/sh = shebang construct (directory to the proper shell interpreter),
directory present by default on unix systems

- read <var_name> = assigns the user input to a new <var_name>

- unset <var_name> = unsets a variable

- readonly = makes a variable "read only" (equivalent to the C "const"> keyword)

- echo <str> = output à la console

- <str> or <str> = string

- `expr <operations>` = output arithmetic operations

- [ $a == $b ] = proper syntax for assignement operations (uses long int)
