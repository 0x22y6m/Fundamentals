## Day 2 - Pointers and Array

Observed little important thing let's see,

```
int arr[10]={10,20,30,40,50,60,70,80,90,100};
 int *ptr=arr;
 
 cout<<*(ptr+1)<<endl;  // output 20 (second element of array)
```

```
int arr[10]={10,20,30,40,50,60,70,80,90,100};
 int *ptr=arr;
 
 cout<<*ptr+1<<endl;  // out 11 (adds 1 to first element of array)
```
- arr[0] -> give value present at 0th index
- &arr[0] -> gives the address of 0th index
- arr     -> gives starting address of an array
- *ptr    -> gives the staring value of an array
-  ptr    -> gives the starting address of an array
-  *(ptr+1) -> refer previous example
-  *prt+1   -> refer previous example
-  1[arr]  -> gives value of first index of an array which works (arr[0] -> *(arr+0) similarly 1[arr] -> *(0+arr) )
















