# Shell scripts I learnt in DevOps Journey.
Just complete basic shell scripting tutorial from this website

https://www.learnshell.org/en/Arrays

## Variables 
Shell variables are created once they are assigned a value. A variable can contain a number, a character or a string of characters. Variable name is case sensitive and can consist of a combination of letters and the underscore "_". Value assignment is done using the "=" sign. Note that no space permitted on either side of = sign when initializing variables.

You can call variable in any new line with $ symbol
```
Name='Akshay'
echo $Name
#output will print Name variable, 
```
Variables can be assigned with the value of a command output. This is referred to as substitution. Substitution can be done by encapsulating the command with `` (known as back-ticks) or with $()

```
FILELIST=`ls`
FileWithTimeStamp=/tmp/my-dir/file_$(/bin/date +%Y-%m-%d).txt
```
Special Variables

$0 - The filename of the current script.

$n - The Nth argument passed to script was invoked or function was called.

$# - The number of argument passed to script or function.

$@ - All arguments passed to script or function.

$* - All arguments passed to script or function.

$? - The exit status of the last command executed.

$$ - The process ID of the current shell. For shell scripts, this is the process ID under which they are executing.

$! - The process number of the last background command.
