## Day 1 of Learning pointer

### pointer ?
pointer is a variable that stores the address of memory location **or** pointer is a variable that store memory address of another variable.

#### Pointer resprentation in linked list
<img width="577" height="386" alt="image" src="https://github.com/user-attachments/assets/b8b8e735-d941-4abb-8441-c81081ed1e72" />

#### Pointer downside
- Accessing arrays and other data structures beyond their bounds
- Referencing automatic variables after they have gone out of existence
- Referencing heap allocated memory after it has been released
- Dereferencing a pointer before memory has been allocated to it

### Declaring Pointers
Pointer variables are declared using a data type followed by an asterisk and then the pointer variable's name
```c
int num;
int *pi;
```

The use of white spaces around the asterisk is irrelevant . The following declartionare all equivalent:
```c
int* pi;
int * pi;
int *pi;
int*pi
```
**The use of white space is a matter of user preference.**

The diagram below represents Three memory location are depicted by three rectangles. The number in the left is address of variable and the three dots represent uninitialized memory.

Pointer to uninitialized memory can be problem, if pointer is dereferned , the pointer probably does not represent a valid address, it may not contain valid data. This will result in program termination on most platforms.

**Memory Diagram**
<img width="264" height="87" alt="image" src="https://github.com/user-attachments/assets/12ebb03e-3d20-4420-958a-ed430756112b" />

The variables num and pi are located at addresses 100 and 104, respectively. Both are assumed to occupy four bytes.

### How to read a Pointer Declaration
The best way to rad pointer declaration is to read them backward.

This a backward declaration.

<img width="358" height="118" alt="image" src="https://github.com/user-attachments/assets/a0f3a4e4-a495-4a14-8a47-3822dd1fb724" />

### Displaying Pointer values
```c
int num=0;
int *pi
pi=&num
cout<<"Address of num" <<&num<<"value " <<num<<endl;
cout << " Address of num " << pi << "value" <<*pi<<endl;
# both gives the same output
```

# Virtual Memory

Virtual Memory and Pointers
1. What is Virtual Memory?

Virtual memory is a memory-management technique provided by the operating system.

It gives each process its own virtual address space. The program works with virtual addresses, while the operating system and CPU translate those addresses to physical memory when needed.

Program
   |
   | Virtual Address
   v
+------------------+
| OS / MMU         |
| Address Mapping  |
+------------------+
   |
   | Physical Address
   v
Physical RAM

Key Point

A pointer in a normal user program contains a virtual address, not a direct physical RAM address.

2. Virtual Address vs Physical Address
Virtual Address

A virtual address is the address that a program uses.

For example:

0x7ffd12345678


When we print a pointer:

int num = 10;
int *pi = &num;

cout << pi << endl;


The address displayed is normally a virtual address.

Physical Address

A physical address identifies a location in the actual RAM hardware.

A normal user program does not directly work with physical RAM addresses.

Virtual Address
      |
      v
Address Translation
      |
      v
Physical Address
      |
      v
RAM

3. Pointers and Virtual Memory

Consider:

int num = 10;
int *pi = &num;


Here:

num
 |
 | value
 v
10


And:

pi
 |
 | contains address of num
 v
&num


Therefore:

pi == &num


And:

*pi == num


The important point is that the address stored in pi is a virtual address in a virtual-memory system.

4. What Happens When We Dereference a Pointer?

When we write:

cout << *pi;


we are asking the system to access the memory represented by the address in pi.

Conceptually:

pi
 |
 | virtual address
 v
Virtual Address
 |
 | Address Translation
 v
Physical Address
 |
 v
RAM
 |
 v
10


The address translation is handled by the system, not manually by the programmer.

5. Pages

Virtual memory is divided into fixed-size blocks called pages.

For example:

Virtual Address Space

+---------+
| Page 0  |
+---------+
| Page 1  |
+---------+
| Page 2  |
+---------+
| Page 3  |
+---------+


A virtual address can be thought of as containing:

Virtual Address
+-------------------+----------------+
| Virtual Page No.  | Page Offset    |
+-------------------+----------------+


The page number identifies the page.

The offset identifies a particular location inside that page.

6. Frames

Physical RAM is divided into blocks called frames.

Pages and frames are the same size.

Virtual Memory              Physical RAM

+---------+                 +---------+
| Page 0  | --------------> | Frame 5 |
+---------+                 +---------+
| Page 1  | --------------> | Frame 2 |
+---------+                 +---------+
| Page 2  | --------------> | Frame 8 |
+---------+                 +---------+
| Page 3  | --------------> | Frame 1 |
+---------+                 +---------+


A virtual page can be placed into different physical frames.

Therefore, a program's pages do not need to be stored next to each other in physical RAM.

7. Page Table

The operating system needs a way to keep track of where each virtual page is located.

It uses a page table.

The basic mapping looks like:

Virtual Page       Physical Frame

Page 0      --->      Frame 5
Page 1      --->      Frame 2
Page 2      --->      Frame 8
Page 3      --->      Frame 1


So:

Virtual Page Number
        |
        v
    Page Table
        |
        v
Physical Frame Number


The page table is used for virtual-to-physical address translation.

8. MMU

MMU stands for:

Memory Management Unit

The MMU is hardware that performs virtual-to-physical address translation and helps enforce memory-access permissions.

Conceptually:

CPU
 |
 | Virtual Address
 v
MMU
 |
 | Translation
 v
Physical Address
 |
 v
RAM


The MMU uses information from page tables to determine where the requested memory is located.

9. Example of Address Translation

Suppose a program uses:

Virtual Page = 5
Offset       = 100


The page table might contain:

Page 5 ---> Frame 12


The system can then use:

Frame 12 + Offset 100


to determine the physical memory location.

The important idea is:

Virtual Page
     |
     v
Page Table
     |
     v
Physical Frame

10. TLB

TLB stands for:

Translation Lookaside Buffer

The TLB is a small, fast cache used to store recently used virtual-page-to-physical-frame translations.

Without a TLB, the system would frequently need to consult the page table.

With a TLB:

CPU
 |
 | Virtual Address
 v
 TLB
 |
 +---- Hit ----> Physical Address
 |
 +---- Miss ---> Page Table
                    |
                    v
              Physical Frame

TLB Hit

The required translation is already in the TLB.

Virtual Page ---> Physical Frame


The translation can be obtained quickly.

TLB Miss

The translation is not currently in the TLB.

The system needs to consult the page table.

11. Page Fault

A page fault happens when a program accesses a virtual page that is not currently available in physical memory and the system needs to handle the situation.

Conceptually:

Program accesses virtual address
              |
              v
        Is page available?
          /          \
        Yes           No
         |             |
         v             v
     Continue      Page Fault
                       |
                       v
                  OS handles it
                       |
                       v
                 Page loaded/mapped
                       |
                       v
                    Continue


A page fault does not automatically mean your program has a bug.

A page can be valid but simply not currently resident in RAM.

12. Swapping

When memory is under pressure, the operating system can move memory pages between RAM and secondary storage.

For example:

RAM

+---------+
| Page A  |
+---------+
| Page B  |
+---------+
| Page C  |
+---------+


The OS may move Page B out of RAM:

RAM                     Storage

+---------+             +---------+
| Page A  |             | Page B  |
+---------+             +---------+
| Page C  |             +---------+
+---------+


Later, Page B can be brought back into RAM.

It may be placed in a different physical frame.

Before:

Page B ---> Frame 3


Later:

Page B ---> Frame 9


The physical location can change while the program continues using its virtual address.

13. Does the Pointer Change?

Suppose:

int num = 10;
int *pi = &num;


Conceptually:

pi
 |
 v
Virtual Address
 |
 v
Page containing num
 |
 v
Physical Frame


If the operating system changes the physical frame:

Before:

Virtual Page ---> Frame 3


Later:

Virtual Page ---> Frame 9


The program continues using the same virtual address.

This is one of the important advantages of virtual memory.

14. Why Virtual Memory Is Useful

Virtual memory provides several benefits:

Each process gets its own virtual address space.
Processes can be isolated from each other.
Memory access permissions can be enforced.
Pages can be stored in non-contiguous physical memory.
The OS can manage physical RAM more flexibly.
Not every virtual page needs to be resident in RAM at the same time.
Memory can be shared between processes when appropriate.
15. Important Difference: Pointer vs Physical Address

Do not think:

Pointer
   |
   v
Physical RAM Address


Instead, use this mental model:

Pointer
   |
   v
Virtual Address
   |
   v
MMU / Address Translation
   |
   v
Physical Address
   |
   v
RAM


This is the most important concept to remember.

16. Pointer Example
#include <iostream>
using namespace std;

int main() {

    int num = 10;
    int *pi = &num;

    cout << "Value of num: " << num << endl;
    cout << "Address of num: " << &num << endl;

    cout << "Value stored in pi: " << pi << endl;
    cout << "Value pointed to by pi: " << *pi << endl;

    return 0;
}


Possible output:

Value of num: 10
Address of num: 0x7ffd12345678
Value stored in pi: 0x7ffd12345678
Value pointed to by pi: 10


Remember:

num     -> value
&num    -> address of num
pi      -> address stored in pi
*pi     -> value at the address stored in pi

17. Important Terms
Term	Meaning
Virtual Memory	Memory abstraction provided by the OS
Virtual Address	Address used by a program
Physical Address	Address/location in physical memory
Page	Fixed-size block of virtual memory
Frame	Fixed-size block of physical memory
Page Table	Maps virtual pages to physical frames
MMU	Hardware that performs address translation
TLB	Cache for recent address translations
Page Fault	Event requiring handling when a needed page isn't currently resident/mapped
Swapping	Moving memory pages between RAM and secondary storage
18. Key Points
A pointer normally contains a virtual address on a modern virtual-memory system.
A virtual address is different from a physical address.
The CPU/MMU translates virtual addresses to physical addresses.
Virtual memory is divided into pages.
Physical memory is divided into frames.
A page can be mapped to different physical frames over time.
Pages don't have to be stored contiguously in physical RAM.
A page table stores virtual-page-to-physical-frame mappings.
A TLB caches recently used address translations.
A page can temporarily be moved out of RAM.
The programmer normally doesn't need to know the physical RAM location of an object.
&num gives the address used to refer to num; pi stores that address.
19. Quick Revision
int num = 10;
int *pi = &num;


Think:

             pi
             |
             v
       Virtual Address
             |
             v
       Page / Page Table
             |
             v
            MMU
             |
             v
      Physical Frame
             |
             v
            RAM
             |
             v
            10

Remember
num   = value
&num  = address
pi    = address
*pi   = value


And:

Pointer → Virtual Address → Translation → Physical Memory

Sources

Loyola University Chicago — Virtual Memory
 — explanation of virtual memory, MMU, pages, page tables, TLB, and page faults.

MIT — Introduction to Paging
 — detailed lecture notes on pages, frames, page tables, TLBs, and address translation.

OpenStax — Memory Management
 — beginner-friendly explanation of virtual memory, address translation, pages, and TLBs.

Dive Into Systems — Virtual Memory
 — detailed explanation of paging, page tables, physical frames, and TLBs.

University of Virginia — Virtual Memory
 — useful for going deeper into page tables and virtual-address translation.



























