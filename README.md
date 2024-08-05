# Shell scripts I learnt in DevOps Journey.
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
