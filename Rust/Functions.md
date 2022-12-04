# FUNCTIONS
---
- `fn` keyword is used to declare a new function
```
fn main() {
    println!("Hello, world!");

    another_function();
}

fn another_function() {
    println!("Another function.");
}
```

Rust doesn’t care where you define your functions, only that they’re defined somewhere in a scope that can be seen by the caller.

## Parameters
We can define functions to have parameters, which are special variables that are part of a function’s signature
```
fn main() {
    another_function(5);
}

fn another_function(x: i32) {
    println!("The value of x is: {x}");
}
```

- Requiring type annotations in function definitions means the compiler almost never needs you to use them elsewhere in the code to figure out what type you mean
- When defining multiple parameters, the parameter declarations are seperated by commas

### Statements and Expressions
- Statements are instructions that perform some action and do not return a value.
- Expressions evaluate to a resulting value

Variable declarations, function declarations are statements
```
fn main() {
    let x = (let y = 6);
}
```
- Code above gives an error as `let` does not return any value

Calling functions, macros and a new scope created by curly brackets are expressions
- Expressions do not have a semicolon at the end. Putting a semicolon turns an expression into a statement

### Return Values
- Return values are not named but their type must be declared using `->` 
- You can return early from a function by using the `return` keyword and specifying a value, but most functions return the last expression implicitly.
```
fn five() -> i32 {
    5
}

fn main() {
    let x = five();

    println!("The value of x is: {x}");
}
```