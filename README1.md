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


