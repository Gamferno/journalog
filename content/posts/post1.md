+++
title = "TIL : Rust Basics"
date = "2025-08-16"
+++

## 🌱 Summary  

Today i Learned about Rust's common programming concepts- Variables and Mutability, Data Types, Functions, Comments and Control Flow

---

## 📓 Journal / Notes  

So basically i started with this [Rust's Programming Language book](https://rust-book.cs.brown.edu), this is the Brown edu version and has additional quizzes within each chapters which is not there in the original

in Variables we see how they are defined like 
```rust
let x = 5;
let x : u32 = 5;
let mut x = 5;
let mut x: u32 = 5;
const x: u32 = 5; // 
```

Things which i found new was that in Rust by default all variable are immutable, i have been a cpp user so this was new for me, also that const must be defined with a data type, which is optional when we use let keyword

In Datatypes, we were introduced to various data types we already know, like for int their is u32, i32, u64, u128 etc. that is basically the limit of no. after which it gives error like u32 can go upto 2^32 -1 but i32 can only go from -2^31 to 2^31 -1 
and their are other datatypes like bool, floating f32 or f64, char type 

```rust
    let x = 2.0; // f64
    let y: f32 = 3.0; // f32

    let t = true;
    let f: bool = false;

    let c = 'z';
    let z: char = 'ℤ'; 
```

Also their was a mention of two types of datatypes that was either scalar - simple data types like floating, int , bool
compound - multiple values 

compond has two data types -> tuple or a array

tuple can store multiple different types of values, and arrays can store multiple values of same type 

```rust
fn main() {
    let tup = (500, 6.4, 1);
    let tup2: (i32, f64, u8) = (500, 6.4, 1);

    let (x, y, z) = tup;

    let five_hundred = tup2.0;

    let six_point_four = tup2.1;
}
```

we deconstruct tuple in the way we did on line 3 of program above with name of variable = tuple or just can the element index number and use that like we did in 4 and 5

As for array, we can initially with datatype and no. of elements or with default value and no. of elements

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5]; // i32
let b = [3; 5]; // [3,3,3,3,3]
```

We already know how to take input but a thing to remeber when converting the String input we took and assigned to our variable we wish to use as index for our array is that keep the to be converted data type as **usize and not u32**, i dont know why but only usize worked

```rust
    let mut index = String::new();

    io::stdin()
        .read_line(&mut index)
        .expect("Failed to read line");

    let index: usize = index
        .trim()
        .parse()
        .expect("Index entered was not a number");
```

in Functions, it was pretty similiar to cpp, just the keyword is fn, we pass parameters, we define data types of parameters and we can also define the data type of return value 

```rust
fn main() {
    let x = plus_one(5);

    println!("The value of x is: {x}");
}

fn plus_one(x: i32) -> i32 {
    x + 1;
}
```

the only new thing to note is that, in Rust we dont write "return", we just write the value and not write a semicolon after that

For the control flow, it is similiar to cpp its just that the rust compiler suggests to remove brackers if used in conditions and suggest to write as it is

```rust
    let number = 3;

    if number != 0 {
        println!("number was something other than zero");
    }
```

like we use ternary operator in cpp, we can do that here like 
```rust
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}");
```

this basically checks if {condition} is true (which it is ) and then returns the value inside its bracket and assigns that to number

Then finally there are loops 
three types -> loop, while loop and for loop

from  what i learned loop is not commonly used as it requires conditioning for breaking , while is also used less oftenly 
and for loop is used 99% of the time

we can do for each loop like this 
```rust
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
```

and a for loop in range (with reverse) like this 
```rust
    for number in (1..4).rev() {
        println!("{number}!");
    }
    println!("LIFTOFF!!!");
```


## 💭 Thoughts

I am mostly understanding Rust and would hope to finish it in next week and start Solana 


