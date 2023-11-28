---
tags:
  - cm12002
  - programming
  - CS
links:
  - "[[Computer Systems Architectures]]"
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

# Example Incorporating Basic Syntax
```c
#include <stdio.h>

// Define a struct for a person
typedef struct {
    char name[50];
    int age;
    float height;
} Person;

// Function declaration
void introduce(Person p);
float average(int a[], int n);

int main() {
    // Variable declaration
    int choice;
    Person john = {"John Doe", 25, 5.9};

    // Loop
    do {
        printf("Menu:\n");
        printf("1. Introduce John\n");
        printf("2. Average of numbers\n");
        printf("3. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        // Conditional
        switch(choice) {
            case 1:
                introduce(john);
                break;
            case 2:
                {
                    int n, i;
                    int numbers[50];
                    
                    printf("How many numbers? ");
                    scanf("%d", &n);
                    
                    printf("Enter %d numbers: ", n);
                    for (i = 0; i < n; i++) {
                        scanf("%d", &numbers[i]);
                    }
                    
                    printf("Average = %.2f\n", average(numbers, n));
                }
                break;
            case 3:
                printf("Goodbye!\n");
                break;
            default:
                printf("Invalid choice!\n");
        }
    } while(choice != 3);

    return 0;
}

// Function definition
void introduce(Person p) {
    printf("Hello! My name is %s. I am %d years old and my height is %.2f meters.\n", p.name, p.age, p.height);
}

float average(int a[], int n) {
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += a[i];
    }
    return (float)sum / n;
}
```
