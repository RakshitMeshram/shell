##  Author : Rakshit Meshram (17213) 
##  Assignment 2 - Operating System
#	   MICROSHELL   

/ What does this shell do ?
This shell performs the basic functionalities like traversing directories, listing directories,
date, time, cat, echo, whoami, uname, su, executing a program in subshell, doesn't quit even after the subshell ends.


/ How does this shell do what it does ?
This shell uses a few inbuilt libraries to implement functions like fork(), execvp(), signal(),wait().

fork() : creates a child process.

execvp() : The created child process does not have to run the same program as the parent process does. The exec type system calls allow a process to run any program files, which include a binary executable or a shell script.
The execvp() system call requires two arguments:
    The first argument is a character string that contains the name of a file to be executed.
    The second argument is a pointer to an array of character strings. More precisely, its type is char \**, which is exactly identical to the argv array used in the main program:
            int  main(int argc, char \**argv)
    Note that this argument must be terminated by a zero.
    When execvp() is executed, the program file given by the first argument will be loaded into the caller's address space and over-write the program there. Then, the second argument will be provided to the program and starts the execution. As a result, once the specified program file starts its execution, the original program in the caller's address space is gone and is replaced by the new program.

    execvp() returns a negative value if the execution fails (e.g., the request file does not exist).

wait() : A call to wait() blocks the calling process until one of its child processes exits or a signal is received. After child process terminates, parent continues its execution after wait system call instruction.
    Child process may terminate due to any of these:

        * It calls exit();
        * It returns (an int) from main
        * It receives a signal (from the OS or another process) whose default action is to terminate.


signal() :  custom signal handlers to “catch” signals and override the default signal handling mechanism.

exit() :  causes process termination.



How to compile this file ?
gcc -Wall -pedantic -static my_shell.c -o mysh

How to run this program ?
./mysh

How to exit out of this program ?
type "exit" or Ctrl + Z   (Note : Ctrl + C will not work. This works only to stop the running processes inside the program.)
A very useful feature : 
    Disable signal SIGNAL in the parent: This means I can interrupt(Ctrl + C) a process without killing my shell.  

Some notable features :
    * Add a visual prompt: $ for users and # for superusers.
    * Print the exit code of the child, e.g. <1> or <0>
    * Check for empty input: Because segfaulting is not nice.
