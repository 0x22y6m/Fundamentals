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


## Virtual Memory
What is Virtual Memory?

Virtual memory is a memory-management technique used by the operating system.

It gives each program its own virtual address space.

A program uses virtual addresses, not direct physical RAM addresses.

```c
Program
   |
   v
Virtual Address
   |
   v
OS / MMU
   |
   v
Physical Address
   |
   v
RAM
```

**Virtual Address**

A virtual address is the address used by a program.

Example:

```0x7ffd12345678```


When we print a pointer, we normally see a virtual address.

```c
int num = 10;
int *pi = &num;

cout << pi << endl;
```

### Physical Address

A physical address refers to the actual location in physical RAM.

A normal program does not directly work with physical addresses.

Virtual Address → Physical Address → RAM

Pointers

Example:

```c
int num = 10;
int *pi = &num;
```

**Remember:**

num    → value of num
&num   → address of num
pi     → address stored in pi
*pi    → value at that address


Because:

```pi = &num;```


we have:

```pi == &num```


and:

```*pi == num```

### Pages and Frames

Virtual memory is divided into pages.

Physical RAM is divided into frames.

```
Virtual Memory          Physical RAM

Page 0  ------------->  Frame 5
Page 1  ------------->  Frame 2
Page 2  ------------->  Frame 8
```

Pages do not need to be stored next to each other in RAM.

### Page Table

A page table keeps track of where virtual pages are located in physical memory.

```
Virtual Page → Physical Frame

Page 0 → Frame 5
Page 1 → Frame 2
Page 2 → Frame 8
```
### MMU

MMU = Memory Management Unit

The MMU helps translate virtual addresses into physical addresses.

```c
Virtual Address
       |
       v
      MMU
       |
       v
Physical Address
       |
       v
      RAM
```

### TLB

TLB = Translation Lookaside Buffer

The TLB is a small, fast cache that stores recently used address translations.

Virtual Page → Physical Frame


It helps make address translation faster.

### Page Fault

A page fault occurs when a program accesses a page that requires the operating system to handle its presence in memory.

The OS handles the situation and, when appropriate, loads/maps the required page.

```
Program
   |
   v
Access Page
   |
   v
Page available?
  / \
Yes  No
 |    |
 v    v
Run  Page Fault
       |
       v
    OS handles it

```
A page fault does not automatically mean there is a bug.

### Swapping

When memory is under pressure, the operating system may move pages between RAM and secondary storage.

```
RAM                 Storage

Page A              Page B
Page C              Page D
```

Later, a page can be brought back into RAM.

Most Important Concept
```
Don't think:

Pointer → Physical RAM


Think:

Pointer
   ↓
Virtual Address
   ↓
Address Translation
   ↓
Physical Memory

Quick Revision
int num = 10;
int *pi = &num;
```

num   → 10
&num  → address of num
pi    → address of num
*pi   → 10
```
Key Terms
Virtual Memory → Memory abstraction provided by the OS
Virtual Address → Address used by a program
Physical Address → Location in physical memory
Page → Block of virtual memory
Frame → Block of physical memory
Page Table → Maps pages to frames
MMU → Performs address translation
TLB → Caches recent address translations
Page Fault → Requires OS memory-management handling
Swapping → Moving pages between RAM and storage
One-Line Summary
```

Pointers contain addresses used by the program; with virtual memory, those addresses are normally virtual addresses that are translated to physical memory by the system.























