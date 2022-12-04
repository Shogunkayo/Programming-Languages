# CONTROL FLOW 
---
The most common constructs that let you control the flow of execution of Rust code are `if` expressions and loops

## `if` Expressions
- An `if` expression allows you to branch your code depending on conditions
- Optionally, we can also include an `else` expression to give the program an alternative block of code to execute should the condition evaluate to false
- The condition provided must evaluate to a `bool`
- Rust will not automatically try to convert non-Boolean types to a Boolean
- Multiple conditions can be handled using `else if`

```
fn main() {
    let number = 6;

    if number % 4 == 0 {
        println!("number is divisible by 4");
    } else if number % 3 == 0 {
        println!("number is divisible by 3");
    } else if number % 2 == 0 {
        println!("number is divisible by 2");
    } else {
        println!("number is not divisible by 4, 3, or 2");
    }
}
```

### Using `if` in `let`
- As `if` is an expression, it can be used to assign values
- The types of the expressions in each `if` arm must be the same
```
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}");
}
```

## Loops
- Rust has three kinds of loops: `loop`, `while`, and `for`

### `loop`
- A `loop` executes a block code over and over again forever or untill its made to stop explicitly (either sending an interrupt signal ^C or using the `break` keyword in code)
```
fn main() {
    loop {
        println!("again!");
    }
}
```
- `continue`  keyword  tells the program to skip any code left in the current iteration and and go to the next iteration
- One of the uses of `loop` is to retry an operation you know might fail  like checking if a thread has completed its job
```
fn main() {

    let mut counter: i32 = 0;
    let result = loop {
        counter += 1;
        
        if counter == 10 {
            break counter * 2;
        }
    };

    println!("Result is {result}");

}
```

- When there are nested loops, we can provide labels to specify which loop `break` and `return` act upon, instead of the innermost loop
```
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
```


### `while`
- While the condition is true, the loop runs
```
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{number}!");

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```
### `for`
```
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
}
```

```
fn main() {
    for number in (1..4).rev() {
        println!("{number}!");
    }
    println!("LIFTOFF!!!");
}
```