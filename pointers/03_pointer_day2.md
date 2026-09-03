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
