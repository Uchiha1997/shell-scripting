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
