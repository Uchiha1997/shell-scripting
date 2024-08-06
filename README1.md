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


