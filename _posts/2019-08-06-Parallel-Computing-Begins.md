Parallel Structure of C/C++ Coding
=================================

Basic knowledge we need to have before we start off...
----------------------------------------------
1. Basic C or C++ knowledge.
2. How to compile C/C++ in Command Line Interface.
3. How to execute linked object in Command Line Interface.
4. Basic knowledge of using Command Line Interace on any linux distribution
5. Using variables in BASH/SHELL

Basic Structure-Algorithm about simple parallel structure coding(MPI)
----------------------------------------------------------------------
1. Initialize MPI Module.
2. Initialize RANK.
3. Initialize Size.
4. Execute the rest of the code, like iteration and simple - command.
5. Finalize MPI Module.

<b>So, it will look like: </b>
```
int main(int argc, char *argv[]) {
    // Basic Variable Declaration
    int rank, size;

    // Initialize MPI Module
    MPI_INIT(&argc, &argv);
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);
    MPI_Comm_size(MPI_COMM_WORLD, &size);

    /* Execute the code - Like Loads of iteration, or a command! */

    // Finalize MPI Module
    MPI_Finalize();

    return 0;
}
```
<div style="page-break-after: always;"></div>

Basic function structure
------------------------
As you see simple-demonstration code above, you will notice that function its argument has
```
int main(int argc, char *argv[])
```
rather than
```
int main(void)
```
Because as you know, we can put many arguments when "run" the object file i.e
```
$ gcc test.c
$ ./a.out argument_one argument_two
```
Something like this. <br/>
Let's look how we run MPI-Compatible object file.
```
$ mpiexec -np 10 ./a.out
```
We passes about 3 more arguments to run ./a.out . <br/>
Think about when 'job' needs to be run as parallel work and you must pass arguments? Are you going to handle arguments by removing "mpiexec -np ~"? No. Then its code would be way much dirtier than you might think.<br/><br/>
So, main reason about using
```
int main(int argc, char *argv[])
```
is to remove pre-arguments like "mpiexec, -np, ~" and correctly receive "needed arguments" ! MPI_Init will do that automatically for you.

<div style="page-break-after: always;"></div>

Including Headers
------------------
Put
```
#include <mpi.h>
```
On include section(Preprocessors)

Initializing MPI Module
------------------------
What will it do?<br/>
* <u><b>It will initialize MPI Module and removes any abudant argument from CLI.</b></u>

Original function:
```
int MPI_Init(int *argc, char ***argv)
```
Default usage:
```
MPI_INIT(&argc, &argv);
```
Where "&argc" is single pointer type of int, "&argv" is triple pointer type of char.<br/><br/>
Refer to "Basic function structure" section when you are not sure about argc/argv.

<div style="page-break-after: always;"></div>

Initializing RANK
------------------
What is Rank?
* <b><u> Rank is kind of processor's number. starting 0 to given size - 1.</b></u> <br/>

What will it do? <br/>
* <b><u> It will set the number of processor's name automatically using given pointer type of int value.</b></u> <br/>

Original Function:
```
int MPI_Comm_rank(MPI_Comm comm, int *rank)
``` 
Default usage:
```
MPI_Comm_rank(MPI_COMM_WORLD, &rank);
```
Where MPI_COMM_WORLD is special type of "MPI_Comm" data, and &rank is single pointer integer type variable. We will talk about MPI_COMM_WORLD and MPI_Comm data type later.

Initializing Size
------------------
What is size?
* <b><u>Sum of whole Processors.</b></u> <br/>
* <b><u>It will return 10 when you give 10 processors to run!</b></u> <br/>

What will it do?<br/>
* <b><u>It will automatically set amount of processor given by user.</b></u> <br/>

Original Function:
```
int MPI_Comm_size(MPI_Comm comm, int *size)
```
Default usage:
```
MPI_Comm_size(MPI_COMM_WORLD, &size);
```
As I mentioned above, we will talk about MPI_COMM_WORLD later. Just use it for now ~ next study.<br/>
&size is single pointer - integer type variable. After this code, echoing size will return total size of processor given by user.

Finalizing module
-----------------
What will it do?<br/>
* <b><u>It will close usage of module.(somewhat similar to cleaning)</b></u> <br/>

Original Function:
```
int MPI_Finalize(void)
```

Default usage:
```
MPI_Finalize();
```
Disclaimer: <b><u>You MUST finalize the MPI Module once you initialize the MPI Module!</u></b>