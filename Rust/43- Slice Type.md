# SLICE TYPE
---
Slices allow you to reference a contiguous sequence of elements in a collection

## String Slice 
A string slice is a reference to a part of a string

```
    let s = String::from("hello world");

    let hello = &s[0..5];
    let world = &s[6..11];
```

- `..` is called the range syntax

```
	let entire = &s[..] //references entire string
```

- `&str` signifies a string slice
- Defining our function to take a string slice as a parameter instead of a reference to a `String`  makes our API more general and useful without losing any functionality
