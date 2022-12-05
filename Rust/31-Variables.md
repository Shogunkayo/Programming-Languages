# VARIABLES AND MUTABILITY
---
- Variables are declared using `let` keyword
```
let x = 10;
```

## Mutability
- By default variables are immutable
- Adding `mut`  makes the variables mutable and conveys intent that there are parts in the program that will change the value of the variable
```
let mut x = 10;
```

## Constants
- Constants are values that are bound to a name and are not allowed to change
- Constants are always immutable
- Naming convention is to write in uppercase
- Must be assigned to a constant expression, not the result of a value that could be compiled only at runtime
```
const X = 10;
```

## Shadowing
- A new variable can be declared with the same name as a previous variable
```
fn main() {
    let x = 5;

    let x = x + 1;

    {
        let x = x * 2;
        println!("Value of x in the inner scope is: {x}");
    }

    println!("The value of x is: {x}");
}
```
- By using `let`, we can perform a few transformations on a value but have the variable be immutable after those transformations have been completed.
- The other difference between `mut` and shadowing is that because we’re effectively creating a new variable when we use the `let` keyword again, we can change the type of the value but reuse the same name.
