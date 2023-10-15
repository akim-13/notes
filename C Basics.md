---
tags: cm12002, programming
---
%%
links:
%%
# C Basics
- C is an **imperative** (as opposed to declarative) **procedural** (as opposed to object-oriented) language.
- The predecessors of C are `BCPL -> B  -> C`.

# Random Things To Remember
- Reserve 3 characters for output: `printf("%3d", var);`
- Reserve 3 characters for output with 2 digits after decimal point: `printf("%3.2f", var)`.
- **Not initialising a variable** will result in a random value being assigned to it.
    ```c
    int a;
    printf("The variable a is %d\n", a);
    a = 7;
    --
    The variable a is -24867
    ```

