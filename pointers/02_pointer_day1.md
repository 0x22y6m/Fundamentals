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



























