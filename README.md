# Basics of Shell Scripting.
Just complete basic shell scripting tutorial from this website

https://www.learnshell.org/en/Arrays

## Variables 
Shell variables are created once they are assigned a value. A variable can contain a number, a character or a string of characters. Variable name is case sensitive and can consist of a combination of letters and the underscore "_". Value assignment is done using the "=" sign. Note that no space permitted on either side of = sign when initializing variables.

You can call variable in any new line with $ symbol
```shell
Name='Akshay'
echo $Name
#output will print Name variable, 
```
Variables can be assigned with the value of a command output. This is referred to as substitution. Substitution can be done by encapsulating the command with `` (known as back-ticks) or with $()

```shell
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

## Arrays
An array can hold several values under one name. Array naming is the same as variables naming. An array is initialized by assign space-delimited values enclosed in ()
```shell
my_array=(apple banana "Fruit Basket" orange)
new_array[2]=apricot # "Fruit Basket" will be replaced with apricot
new_array[4]=mango # mango will be added as 5th element
```
The total number of elements in the array is referenced by ${#arrayname[@]}
```shell
my_array=(apple banana "Fruit Basket" orange)
echo  ${#my_array[@]}                   # 4
```
The array elements can be accessed with their numeric index. The index of the first element is 0.
```shell
my_array=(apple banana "Fruit Basket" orange)
echo ${my_array[3]}                     # orange - note that curly brackets are needed
# adding another array element
my_array[4]="carrot"                    # value assignment without a $ and curly brackets
echo ${#my_array[@]}                    # 5
echo ${my_array[${#my_array[@]}-1]}     # carrot
```
## Basic Operators
Simple arithmetics on variables can be done using the arithmetic expression: $((expression))
```shell
A=3
B=$((100 * $A + 5)) # 305
```
The basic operators are:

a + b addition (a plus b)

a - b substraction (a minus b)

a * b multiplication (a times b)

a / b division (integer) (a divided by b)

a % b modulo (the integer remainder of a divided by b)

a ** b exponentiation (a to the power of b)

## Basic String Operations
### String Length
```shell
#       1234567890123456
STRING="this is a string"
echo ${#STRING}            # 16
```
### Index
Find the numerical position in $STRING of any single character in $SUBSTRING that matches. Note that the 'expr' command is used in this case.

```shell
STRING="this is a string"
SUBSTRING="hat"
expr index "$STRING" "$SUBSTRING"     # 1 is the position of the first 't' in $STRING
```
### Substring Extraction
Extract substring of length $LEN from $STRING starting after position $POS. Note that first position is 0.

```shell
STRING="this is a string"
POS=1
LEN=3
echo ${STRING:$POS:$LEN}   # his
```

If :$LEN is omitted, extract substring from $POS to end of line

```shell
STRING="this is a string"
echo ${STRING:1}           # $STRING contents without leading character
echo ${STRING:12}          # ring
```
### Substring Replacement
```shell
STRING="to be or not to be"
```
Replace first occurrence of substring with replacement
```shell
STRING="to be or not to be"
echo ${STRING[@]/be/eat}        # to eat or not to be
```
Replace all occurrences of substring
```shell
STRING="to be or not to be"
echo ${STRING[@]//be/eat}        # to eat or not to eat
```
Delete all occurrences of substring (replace with empty string)
```shell
STRING="to be or not to be"
echo ${STRING[@]// not/}        # to be or to be
```
Replace occurrence of substring if at the beginning of $STRING
```shell
STRING="to be or not to be"
echo ${STRING[@]/#to be/eat now}    # eat now or not to be
```
Replace occurrence of substring if at the end of $STRING
```shell
STRING="to be or not to be"
echo ${STRING[@]/%be/eat}        # to be or not to eat
```
Replace occurrence of substring with shell command output
```shell
STRING="to be or not to be"
echo ${STRING[@]/%be/be on $(date +%Y-%m-%d)}    # to be or not to be on 2012-06-14
```
## Decision Making (if loop)

The basic conditional decision making construct(syntax) is:
```shell
if [ expression ]; then

run code if 'expression' is true

fi
```
```shell
NAME="John"
if [ "$NAME" = "John" ]; then
  echo "True - my name is indeed John"
fi
```
It can be expanded with 'else'
```shell
NAME="Bill"
if [ "$NAME" = "John" ]; then
  echo "True - my name is indeed John"
else
  echo "False"
  echo "You must mistaken me for $NAME"
fi
```
It can be expanded with 'elif' (else-if)
```shell
NAME="George"
if [ "$NAME" = "John" ]; then
  echo "John Lennon"
elif [ "$NAME" = "George" ]; then
  echo "George Harrison"
else
  echo "This leaves us with Paul and Ringo"
fi
```
The expression can be a single string or variable.
A empty string or a string consisting of spaces or an undefined variable name, are evaluated as false. 
The expression can be a logical combination of comparisons: 
negation is denoted by !, 
logical AND (conjunction) is denoted by &&, and 
logical OR (disjunction) is denoted by ||. 

### Types of numeric comparisons
```shell
comparison    Evaluated to true when
$a -lt $b    $a < $b
$a -gt $b    $a > $b
$a -le $b    $a <= $b
$a -ge $b    $a >= $b
$a -eq $b    $a is equal to $b
$a -ne $b    $a is not equal to $b
```
### Types of string comparisons
```shell
comparison    Evaluated to true when
"$a" = "$b"     $a is the same as $b
"$a" == "$b"    $a is the same as $b
"$a" != "$b"    $a is different from $b
-z "$a"         $a is empty
```
note1: whitespace around = is required in expression of if loop.
note2: use "" around string variables to avoid shell expansion of special characters as *

### Logical combinations
```shell
if [[ $VAR_A[0] -eq 1 && ($VAR_B = "bee" || $VAR_T = "tee") ]] ; then
    command...
fi
```
### Case Structure
```shell
case "$variable" in
    "$condition1" )
        command...
    ;;
    "$condition2" )
        command...
    ;;
esac
```
Simple case bash structure
```shell
mycase=1
case $mycase in
    1) echo "You selected bash";;
    2) echo "You selected perl";;
    3) echo "You selected phyton";;
    4) echo "You selected c++";;
    5) exit
esac
```
## Loops
### bash for loop
```shell
# basic construct
for arg in [list]
do
 command(s)...
done
```
For each pass through the loop, arg takes on the value of each successive value in the list. Then the command(s) are executed.
```shell
# loop on array member
NAMES=(Joe Jenny Sara Tony)
for N in ${NAMES[@]} ; do
  echo "My name is $N"
done

# loop on command output results
for f in $( ls prog.sh /etc/localtime ) ; do
  echo "File is: $f"
done
```
### bash while loop
```shell
# basic construct
while [ condition ]
do
 command(s)...
done
```
The while construct tests for a condition, and if true, executes commands. It keeps looping as long as the condition is true.
```shell
COUNT=4
while [ $COUNT -gt 0 ]; do
  echo "Value of count is: $COUNT"
  COUNT=$(($COUNT - 1))
done
```
### Bash until loop
```shell
# basic construct
until [ condition ]
do
 command(s)...
done
```
The until construct tests for a condition, and if false, executes commands. It keeps looping as long as the condition is false (opposite of while construct)
```shell
COUNT=1
until [ $COUNT -gt 5 ]; do
  echo "Value of count is: $COUNT"
  COUNT=$(($COUNT + 1))
done
```
### "break" and "continue" statements
break and continue can be used to control the loop execution of for, while and until constructs. continue is used to skip the rest of a particular loop iteration, whereas break is used to skip the entire rest of loop. A few examples:
```shell
# Prints out 0,1,2,3,4

COUNT=0
while [ $COUNT -ge 0 ]; do
  echo "Value of COUNT is: $COUNT"
  COUNT=$((COUNT+1))
  if [ $COUNT -ge 5 ] ; then
    break
  fi
done

# Prints out only odd numbers - 1,3,5,7,9
COUNT=0
while [ $COUNT -lt 10 ]; do
  COUNT=$((COUNT+1))
  # Check if COUNT is even
  if [ $(($COUNT % 2)) = 0 ] ; then
    continue
  fi
  echo $COUNT
done
```
## Shell Functions
Like other programming languages, the shell may have functions. A function is a subroutine that implements a set of commands and operations. It is useful for repeated tasks.
```shell
# basic construct
function function_name {
  command...
}
```
Functions are called simply by writing their names. A function call is equivalent to a command. Parameters may be passed to a function, by specifying them after the function name. The first parameter is referred to in the function as $1, the second as $2 etc.
```shell
function function_B {
  echo "Function B."
}
function function_A {
  echo "$1"
}
function adder {
  echo "$(($1 + $2))"
}

# FUNCTION CALLS
# Pass parameter to function A
function_A "Function A."     # Function A.
function_B                   # Function B.
# Pass two parameters to function adder
adder 12 56                  # 68
```
# Create, View, and Edit Text Files
## Redirect Output to a File or Program
Objectives: Save output or errors to a file with shell redirection, and process command output through multiple command-line programs with pipes.

![alt text](https://rol.redhat.com/rol/static/static_file_cache/rh124-9.0/edit/descriptor-overview.svg)

Standard input (channel 0) reads input from the keyboard. 
Standard output (channel 1) sends normal output to the terminal. 
Standard error (channel 2) sends error messages to the terminal.
If a program opens separate connections to other files, then it might use higher-numbered file descriptors.

| Number        | Channel name  |Description   | Default connection |Usage                |
| ------------- | ------------- |------------- | ------------------ |---------------------|
| 0             | stdin         |Content Cell  | Keyboard           |Read only            |
| 1             | stdout        |Content Cell  | Terminal           |Write only           |
| 2             | stderr        |Content Cell  | Terminal           |Write only           |
| 3+            | filename      |Content Cell  | None               |Read, write, or both |

### Redirect Output to a File

If you redirect stdout to a file and the file does not exist, then the file is created. If the file does exist and the redirection does not append to the file, then the redirection overwrites the file's contents. To discard the output of a process, you can redirect to the empty /dev/null special file that discards channel output that is redirected to it.

As viewed in the following table, redirecting only stdout does not suppress displaying stderr error messages on the terminal.

#### Table 5.2. Output Redirection Operators

##### 1) >file this command Redirect stdout to overwrite a file.

![alt text](https://rol.redhat.com/rol/static/static_file_cache/rh124-9.0/edit/redirection-overview.svg)

##### 2) >>file this command Redirect stdout to append to a file.

![alt text](https://rol.redhat.com/rol/static/static_file_cache/rh124-9.0/edit/redirection-append.svg)

##### 3) 2>file this command Redirect stderr to overwrite a file.

![alt text](https://rol.redhat.com/rol/static/static_file_cache/rh124-9.0/edit/redirection-error.svg)

##### 4) >file this command Redirect stdout to overwrite a file.

![alt text](https://rol.redhat.com/rol/static/static_file_cache/rh124-9.0/edit/redirection-overview.svg)

##### 5) 2> /dev/null this command Redirect stdout to overwrite a file.

![alt text](https://rol.redhat.com/rol/static/static_file_cache/rh124-9.0/edit/combine-overwrite.svg)

##### 6) > file 2>&1 this command Redirect stdout and stderr to overwrite the same file.

![alt text](https://rol.redhat.com/rol/static/static_file_cache/rh124-9.0/edit/combine-overwrite.svg)

##### 7) >> file 2>&1 this command Redirect stdout and stderr to append to the same file.

![alt text](https://rol.redhat.com/rol/static/static_file_cache/rh124-9.0/edit/combine-append.svg)

## Construct Pipelines
A pipeline is a sequence of one or more commands that are separated by the vertical bar character (|). A pipeline connects the standard output of the first command to the standard input of the next command.

The following list shows some pipeline examples:

Redirect the output of the ls command to the less command to display it on the terminal one screen at a time.
```shell
[user@host ~]$ ls -l /usr/bin | less
```
Redirect the output of the ls command to the wc -l command, which counts the number of received lines from ls and prints that value to the terminal.
```shell
[user@host ~]$ ls | wc -l
```
### Pipelines, Redirection, and Appending to a File

When you combine redirection with a pipeline, the shell sets up the entire pipeline first, and then it redirects the input/output. If you use output redirection in the middle of a pipeline, then the output goes to the file and not to the next command in the pipeline.

![alt text](https://rol.redhat.com/rol/static/static_file_cache/rh124-9.0/edit/pipe-tee.svg)

The tee command overcomes this limitation. In a pipeline, tee copies its standard input to its standard output and also redirects its standard output to the files that are given as arguments to the command. If you imagine data as water that flows through a pipeline, then you can visualize tee as a "T" joint in the pipe that directs output in two directions

#### Pipeline Examples with the tee Command

The next example redirects the output of the ls command to the /tmp/saved-output file and passes it to the less command, so it is displayed on the terminal one screen at a time.
```shell
[user@host ~]$ ls -l | tee /tmp/saved-output | less
```
If you use the tee command at the end of a pipeline, then the terminal shows the output of the commands in the pipeline and saves it to a file at the same time.
```shell
[user@host ~]$ ls -t | head -n 10 | tee /tmp/ten-last-changed-files
```
Use the tee command -a option to append the content to a file instead of overwriting it.
```shell
[user@host ~]$ ls -l | tee -a /tmp/append-files
```
# Manage Local Users and Groups

#### What is User?

User accounts are fundamental to system security. Every process (running program) on the system runs as a particular user. Every file has a particular user as its owner. With file ownership, the system enforces access control for users of the files. The user that is associated with a running process determines the files and directories that are accessible to that process.

User accounts are of the following main types: the superuser, system users, and regular users.

1) The superuser account administers the system. The superuser name is root and the account has a UID of 0. The superuser has full system access.

2) The system user accounts are used by processes that provide supporting services. These processes, or daemons, usually do not need to run as the superuser. They are assigned non-privileged accounts to secure their files and other resources from each other and from regular users on the system. Users do not interactively log in with a system user account.

3) Most users have regular user accounts for their day-to-day work. Like system users, regular users have limited access to the system.

Use the id command to show information about the currently logged-in user:
```shell
[user01@host ~]$ id
uid=1000(user01) gid=1000(user01) groups=1000(user01) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```
Use the id command to show information about the currently logged-in user:
```shell
[user01@host ~]$ id
uid=1000(user01) gid=1000(user01) groups=1000(user01) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```
To view information about another user, pass the username to the id command as an argument:
```shell
[user01@host ~]$ id user02
uid=1002(user02) gid=1001(user02) groups=1001(user02) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```
Use the ls -l command to view the owner of a file. 
```shell
[user01@host ~]$ ls -l mytextfile.txt
-rw-rw-r--. 1 user01 user01 0 Feb  5 11:10 mytextfile.txt
```
Use the ls -ld command to view the owner of a directory.
```shell
[user01@host]$ ls -ld Documents
drwxrwxr-x. 2 user01 user01 6 Feb  5 11:10 Documents
```
Use the ps command to view process information.
Use the ps command -a option to view all processes with a terminal. 
Use the ps command -u option to view the user that is associated with a process.
In the following output, the first column shows the username.

```shell
[user01@host ~]$ ps -au
USER     PID %CPU %MEM    VSZ   RSS TTY    STAT START  TIME COMMAND
root    1690  0.0  0.0 220984  1052 ttyS0  Ss+  22:43  0:00 /sbin/agetty -o -p -- \u --keep-baud 1
user01  1769  0.0  0.1 377700  6844 tty2   Ssl+ 22:45  0:00 /usr/libexec/gdm-x-session --register-
user01  1773  1.3  1.3 528948 78356 tty2   Sl+  22:45  0:03 /usr/libexec/Xorg vt2 -displayfd 3 -au
user01  1800  0.0  0.3 521412 19824 tty2   Sl+  22:45  0:00 /usr/libexec/gnome-session-binary
user01  3072  0.0  0.0 224152  5756 pts/1  Ss   22:48  0:00 -bash
user01  3122  0.0  0.0 225556  3652 pts/1  R+   22:49  0:00 ps -au
```
Each line in the /etc/passwd file contains information about one user. The file is divided into seven colon-separated fields. An example of a line from /etc/passwd follows:

```shell
[user01@host ~]$ cat /etc/passwd
...output omitted...
user01:x:1000:1000:User One:/home/user01:/bin/bash
```

Consider each part of the code block, separated by a colon:

1) user01 : The username for this user.

2) x : The user's encrypted password was historically stored here; it is now a placeholder.

3) 1000 : The UID number for this user account.

4) 1000 : The GID number for this user account's primary group. Groups are discussed later in this section.

5) User One : A brief comment, description, or the real name for this user.

6) /home/user01 : The user's home directory, and the initial working directory when the login shell starts.

7) /bin/bash : The default shell program for this user that runs at login. Some accounts use the /﻿sbin/nologin shell to disallow interactive logins with that account.

#### What Is a Group?
A group is a collection of users that need to share access to files and other system resources. Groups can grant access to files to a set of users instead of to a single user.

Each line in the /etc/group file contains information about one group. Each group entry is divided into four colon-separated fields. An example of a line from /etc/group follows:
```shell
[user01@host ~]$ cat /etc/group
...output omitted...
group01:x:10000:user01,user02,user03
```
Consider each part of the code block, separated by a colon:

1) group01 : Name for this group.

2) x : Obsolete group password field; it is now a placeholder.

3) 10000 : The GID number for this group (10000).

4) user01,user02,user03 : A list of users that are members of this group as a supplementary group.

#### Primary Groups and Supplementary Groups

Every user has exactly one primary group. For local users, this group is listed by GID in the /etc/passwd file. The primary group owns files that the user creates.

When a regular user is created, a group is created with the same name as the user, to be the primary group for the user. The user is the only member of this User Private Group. This group membership design simplifies the management of file permissions, to have user groups separated by default.

Users might also have supplementary groups. Membership in supplementary groups is stored in the /etc/group file.
