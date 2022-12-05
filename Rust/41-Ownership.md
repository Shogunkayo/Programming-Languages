# OWNERSHIP
---
- Set of rules that govern how a Rust program manages memory
- Memory is managed through a system of ownership with a set of rules that the compiler checks.

> Both the stack and the heap are parts of memory available to your code to use at runtime, but they are structured in different ways. The stack stores values in the order it gets them and removes the values in the opposite order. This is referred to as _last in, first out_.
> The heap is less organized: when you put data on the heap, you request a certain amount of space. The memory allocator finds an empty spot in the heap that is big enough, marks it as being in use, and returns a _pointer_, which is the address of that location. This process is called _allocating on the heap_ and is sometimes abbreviated as just _allocating_ (pushing values onto the stack is not considered allocating). Because the pointer to the heap is a known, fixed size, you can store the pointer on the stack, but when you want the actual data, you must follow the pointer.
> Pushing to the stack is faster than allocating on the heap because the allocator never has to search for a place to store new data; that location is always at the top of the stack. Comparatively, allocating space on the heap requires more work, because the allocator must first find a big enough space to hold the data and then perform bookkeeping to prepare for the next allocation.
> Accessing data in the heap is slower than accessing data on the stack because you have to follow a pointer to get there.

## Ownership Rules
- Each value in Rust has an owner
- There can be only one owner at a time
- When the owner goes out of scope, the value will be dropped

## Variable Scope

```
let x = "Hello";
```

The variable `x` refers to a string literal, where the value of the string is hardcoded into the text of our program. The variable is valid from the point at which it’s declared until the end of the current scope.

## String Type
- String literals are hardcoded and are immutable
- String type `String` manages data allocated on the heap and hence can store an amout that is unkown at compile time.
- `String` can be mutable
```
let mut x = String::from("Hello");
x.push_str(" World");
```

## Memory and Allocation
- In case of a string literal, we know the contents at compile time
- String literals are fast and efficient as they are immutable
- For a `String` type, 
	- The memory must be requested from the memory allocator at runtime.
	- We need a way of returning this memory to the allocator when we’re done with our `String`.
- Allocating memory is done by `String::from`

>However, the second part is different. In languages with a _garbage collector (GC)_, the GC keeps track of and cleans up memory that isn’t being used anymore, and we don’t need to think about it. In most languages without a GC, it’s our responsibility to identify when memory is no longer being used and call code to explicitly free it, just as we did to request it. Doing this correctly has historically been a difficult programming problem. If we forget, we’ll waste memory. If we do it too early, we’ll have an invalid variable. If we do it twice, that’s a bug too. We need to pair exactly one `allocate` with exactly one `free`.

- In Rust, the memory is automatically returned once the variable that owns it goes out of scope
```
{
	let x = String::from("Hello"); // x is valid from now
	// do stuff with x
}                                  // x is no longer valid
```
- When a variable goes out of scope, Rust calls a special function`drop` to return the memory

## Data and Variable Interaction

### 1.  _Move_
- When dealing with the stack,
```
let x = 5;
let y = x;
```
As integers are known values, `x` and `y` are assigned to `5` and are pushed onto the stack

- When dealing with `String`
```
let s1 = String::from("hello");
let s2 = s1;
```

 A `String` is made up of three parts: a pointer to the memory that holds the contents of the string, a length, and a capacity. This group of data is stored on the stack.. The contents of the pointer are stored on the heap

- Length is how much memory, in bytes, the contents of `String` is currently using
- Capacity is the total amount of memory `String` has received from the allocator

When `s2` is assigned to `s1`, the data on the stack is copied, but not the data on the heap. If the data on the heap was copied, it would be very expensive in terms of runtime performance if the data on the heap was huge

As stated earlier, when a variable goes out of scope, `drop` is called which tries to deallocate memory. When `s2` is assigned to `s1`, the pointer field of both the variables point to the same location in the heap. To ensure that the same memory is not freed more than once, after the line `let s2 = s1`,  Rust considers `s1` as no longer valid.

```
let s1 = String::from("hello");
let s2 = s1;

println!("{}, world!", s1); //returns error as s1 is invalid
```

When `let s2 = s1` is done, we say `s1` was _moved_ to `s2`

### 2. _Clone_
- To copy the heap data as well as the stack data, `clone` method is used 
```
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {}, s2 = {}", s1, s2);
```
- This may be expensive, depending on the size at runtime

### 3. Copy
```
let x = 5;
let y = x;

println!("x = {}, y = {}", x, y);
```

Rust has a special annotation called the `Copy` trait that we can place on types that are stored on the stack, as integers are. If a type implements the `Copy` trait, variables that use it do not move, but rather are trivially copied, making them still valid after assignment to another variable.

List of types that implement `Copy`: 
- All the integer types, such as u32.
- The Boolean type, bool, with values true and false.
- All the floating point types, such as f64.
- The character type, char.
- Tuples, if they only contain types that also implement Copy. For example, (i32, i32) implements Copy, but (i32, String) does not.

## Ownership and Functions
![[u43.png]]

### Returning values
![[u44.png]]

- In case we want to return another value along with the ownership, we can use a tuple
```
fn takes_and_gives_multiple (temp: String) -> (String, usize) {
    let length = temp.len();
    (temp, length)
}
```

There is a way to pass values without transfering ownership called _references_
