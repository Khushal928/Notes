
At an instant, lot of processes will be there (obviously), but sadly we are limited with one CPU. So all the processes are run one after another for a small amount of time and then the next one, back and forth, so that feel of running all the processes at same time is achieve. this is called time sharing the CPU and this is how virtualization the CPU is achieve. 

Issues
-  Performance
-  Control

**Why control issues:**
-  all the processes have their own stack and heap loaded in RAM
-  all the threads in a single process share same heap but different stack
- basically, CPU can access all the storage in RAM, and any process should not be ask CPU to look at memory of any other process
-  also CPU should not be given to a single process all the time
-  which means kernel should be in control over CPU.
// TODO  what is memory map, how is cpu given all the address of what all it can access


**Basic Technique: Limited Direct Execution**
when kernel wants to execute a process, it creates a process entry in process list, allocates some memory to it and starts executing main or whatever similar .

![[Pasted image 20260210230046.png]]

BUT 
- how will OS know if this little process doesn't do what it is supposed to do i.e; how does it know if its doing something correct
- above method only stops when program returns something. but kernel should have power if it requires some other process to run over.

**How to restrict any process**
user mode is restricted with what it can do, example - a code can't make I/O request to disk
while in kernel mode, more privileged

when ever a user program wants to get some privilege, if program performs a system call, this call allows the kernel to expose certain features required to complete user program. 
it gives lot of power including:
accessing the file system, creating and destroying processes, communicating with other processes, and allocating more memory.

- most OS provide few 100's of such calls

---------------------------------------------

Ideally, if a process relies just on its allocated stack, heap, other allocated resources but when following happens, the process go / get forced to jump into kernel mode

	1) System calls, code asks for more privileges no  