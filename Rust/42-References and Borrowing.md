# REFERENCES and BORROWING
---
A reference is equivalent to a pointer that is guranteed to point to a valid value of a particular type for the life of that reference
- Represented by `&`
- References allow you to refer to a value without taking ownership of it
- `*` is used for deferencing

```
fn main (){
	let s6 = String::from("Hello");
    let length = does_not_take(&s6);
    println!("{length}");
}

fn does_not_take(temp: &String) -> usize {
	temp.len()
}
```

The act of creating a reference is called _borrowing_. Trying to modify reference will not work. Just as varaibles are immutable by default, so are references

```
fn change(temp: &String) {
	temp.push_str("World");
}
```

Both the variable and the reference must be made mutable. Mutable references have one big restriction that a mutable value can have only one mutable reference. This restriction prevents _data races_ ( similar to _race conditions_)
```
fn main() {
	let mut s6 = String::from("Hello");
	change(&mut s6);
	println!("{s6}");
}

fn change(temp: &mut String) {
	temp.push_str(" World");
}
```

```
    let mut s = String::from("hello");

    {
        let r1 = &mut s;
    } // r1 goes out of scope here, so we can make a new reference with no problems.

    let r2 = &mut s;
```

- A mutable variable cannot have both mutable and immutable references simultaneously. 
- It can have either multiple immutable references or one mutable reference

## Reference Scope 
A reference's scope starts from where it is introduced and continues through the last time that reference is used 
```
    let mut s = String::from("hello");

    let r1 = &s; // no problem
    let r2 = &s; // no problem
    println!("{} and {}", r1, r2);
    // variables r1 and r2 will not be used after this point

    let r3 = &mut s; // no problem
    println!("{}", r3);
```

The ability of the compiler to tell that a reference is no longer being used at a point before the end of the scope is called _Non-Lexical Lifetimes_

## Dangling References 
In Rust, the compiler gurantees that references will never be dangling references

```
fn dangle() -> &String { // dangle returns a reference to a String

    let s = String::from("hello"); // s is a new String

    &s // we return a reference to the String, s
} // Here, s goes out of scope, and is dropped. Its memory goes away.
  // Danger!
```