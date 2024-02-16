---
tags:
  - cm12002
  - programming
  - CS
links:
  - "[[Computer Systems Architectures]]"
  - "[[C Basics]]"
presentations:
  - W20_L01_P01
---
# C Pointers
- A **pointer** is a variable that holds the memory address of another variable, enabling direct access and manipulation of its value in memory. In other words, a pointer is just *an address of another variable*.

```c
#include <stdio.h>

void swap(int* a, int* b) 
{
    printf("Pointer to the 1st number: %d\n", a);
    printf("Pointer to the 2nd number: %d\n", b);
    int tmp = *a;
    *a = *b;
    *b = tmp;
}

void deepCopy(char *dst, char *src, int len)
{
    while(len--)
        *dst++ = *src++;
}

int main() {
    int x = 10;
    int y = 20;
    printf("x = %d\ny = %d\n", x, y);

    // `&` means "the address of":
    printf("\nThe address of x is: &x = %d\n", &x);

    // To declare a pointer means to declare a variable that contains the 
    // address of another variable of specified type. Declaration does not
    // dereference the variable. 
    // The following pointer declarations are equivalent. I prefer the 
    // first one, since it is distinct from the dereferencing operation.
    int* ptr = &x;
    int * ptr1 = &x;
    int *ptr2 = &x;

    // Be aware that the following declares 
    // one pointer (a) and one integer (b):
    int* a, b;
    // When declaring multiple pointers at once
    // the following syntax must be used:
    long *c, *d;

    // The simplest pointer is the NULL pointer, which points to nothing.
    // Dereferencing such pointer will cause a segmentation fault.
    d = NULL;

    // `*` is the dereferencing operator that accesses the contents 
    // of the variable, which address the pointer is pointing to.
    printf("Pointer ptr, which points to x: ptr = %d\n", ptr);
    printf("Dereferenced ptr, which points to x: *ptr = %d\n", *ptr);

    // Example of passing by reference.
    printf("\nBefore swap: x = %d, y = %d\n", x, y);
    swap(&x, &y);
    printf("After swap: x = %d, y = %d\n", x, y);
     
    // All pointers have the same size, since pointers are just addresses:
    printf("\nSize of int* a: %d\n", sizeof(a));
    printf("Size of long* c: %d\n", sizeof(c));

    // Pointer arithmetic is possible, however it behaves differently.
    // E.g. incrementing a pointer by 1 increases it 
    // by the size of the type it is pointing at:
    printf("\nsizeof(int) = %d\n", sizeof(int));
    printf("Pointer to int (ptr): %d\n", ptr);
    printf("++ptr: %d\n", ++ptr);
    printf("ptr = ptr + 2: %d\n", ptr = ptr + 2);

    // Pointers can point to other pointers:
    int* ptrToX = &x;
    int** ptrToPtrToX = &ptrToX;
    printf("\nx: %d\n*ptrToX: %d\n**ptrToPtrToX: %d\n", x, *ptrToX, **ptrToPtrToX);

    // The actual array variable is a pointer to the start of the array.
    // Therefore, the syntax for accessing an element of an array `arr[i]`
    // is a shorthand for dereferencing a pointer `*(arr + i)`.
    char arr[6] = {'h', 'e', 'l', 'l', 'o', '\0'};
    printf("\narr = 'hello'\n");
    printf("arr[2]: %c\n", arr[2]);
    printf("*(arr + 2): %c\n", *(arr + 2));
    // However, array pointers are constants, their values cannot 
    // be changed during execution once defined. E.g. `arr++;` will 
    // cause a compilation error.

    // To create a shallow copy of an array, copy the pointer to it:
    char* arrShallowCopy = arr;
    // To create a deep copy use a helper function:
    char arrDeepCopy[6];
    deepCopy(arrDeepCopy, arr, 6);

    arrDeepCopy[0] = '\0';
    printf("\narr[0] after changing arrDeepCopy[0] = '\\0': %c\n", arr[0]);
    arrShallowCopy[0] = '\0';
    printf("arr[0] after changing arrShallowCopy[0] = '\\0': %c\n", arr[0]);
    
    return 0;
}
---
$ gcc pointers.c && ./pointers.c 
x = 10
y = 20

The address of x is: &x = -1096449512
Pointer ptr, which points to x: ptr = -1096449512
Dereferenced ptr, which points to x: *ptr = 10

Before swap: x = 10, y = 20
Pointer to the 1st number: -1096449512
Pointer to the 2nd number: -1096449508
After swap: x = 20, y = 10

Size of int* a: 8
Size of long* c: 8

sizeof(int) = 4
Pointer to int (ptr): -1096449512
++ptr: -1096449508
ptr = ptr + 2: -1096449500

x: 20
*ptrToX: 20
**ptrToPtrToX: 20

arr = 'hello'
arr[2]: l
*(arr + 2): l

arr[0] after changing arrDeepCopy[0] = '\0': h
arr[0] after changing arrShallowCopy[0] = '\0':
```

