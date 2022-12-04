# DATA TYPES
---
- 2 subsets - scalar and compound 
- Rust is a statically typed language, it must know the types of all variables at compile time
- When many types are possible, we add a type annotation
- Unless type casting, adding annotations are optional. If there is no annotation, the compiler considers the default type

## Scalar
- Represents a single value

### Integer
- Number without a fractional component 

| Length  | Signed | Unsigned |
| ------- | ------ | -------- |
| 8-bit   | i8     | u8       |
| 16-bit  | i16    | u16      |
| 32-bit  | i32    | u32      |
| 64-bit  | i64    | u64      |
| 128-bit | i128   | u128     |
| arch    | isize  | usize    | 

- Signed numbers are stored using two's complement representation
- `isize` and `usize` types depend on the architecture of the computer your program is running on, which is denoted in the table as “arch”: 64 bits if you’re on a 64-bit architecture and 32 bits if you’re on a 32-bit architecture.
- Number literals can use `_` as a visual seperator. For example`1_000` is equal to `1000`
- Integer types default to `u32`
- The primary situation in which you’d use `isize` or `usize` is when indexing some sort of collection
- Integer divions rounds down to the nearest integer

### Floating-Point
- Rust’s floating-point types are `f32` and `f64`, which are 32 bits and 64 bits in size, respectively
- `f64` is the default as it is capable of more precision
- All floating-point types are signed
- The `f32` type is a single-precision float, and `f64` has double precision.
```
let x: f32 = 10.00;
```

### Boolean
- A Boolean type in Rust has two possible values: `true` and `false`
- Booleans are 1 byte in size
- Specified using `bool`
```
let x: bool = true;
```

### Character
- `char` is the language's most primitive alphabetic type
```
let x: char = 'X';
```
- `char` literals are specified with single quotes
- 4 bytes in size and represents a Unicode Scalar Value, which means it can represent a lot more than just ASCII. Accented letters; Chinese, Japanese, and Korean characters; emoji; and zero-width spaces are all valid `char` values in Rust


## Compound 
- Compound types can group multiple values into a single type

### Tuple
- Have fixed length
- We create a tuple by writing a comma-separated list of values inside parentheses
- The types of individual elements can be different
```
let tup: (i32, f64, u8) = (500, 6.4, 1);
```
- The elements can be accessed directly by the dot operator followed by the index
```
let x = tup.0;
```
- To destructure a tuple,
```
let tup = (500, 6.4, 1);
let (x, y, z) = tup;
println!("The value of y is: {y}");
```
- A `unit` is a tuple without any values. This value and the corresponding type are both `()` and represent an empty value or an empty return type
- Expressions generally return a `unit` if they don't return any other value

### Array
- Every element of an array must have the same type
- Arrays have a fixed length
- We write the values in an array as a comma-separated list inside square brackets
```
let x: [u32; 4] = [10, 20, 30, 40];
```
- An array can be initialized to contain the same value for each element by specifying the initial value, followed by a semicolon, and then the length of the array in square brackets
```
let x = [3; 4];
```
- To access an element,
```
let x0 = x[0];
```