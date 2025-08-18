+++
title = "TIL : Rust Ownership + Typescript Basics"
date = "2025-08-18"
+++

## 🌱 Summary  

Today i studied Rust Ownership concepts -> References and Ownerships & Borrowing and intro to Typescript

---

## 📓 Journal / Notes  

In Rust, yesterday i read the intro to ownership from the rust book, in very brief if i have to tell Ownership s ensuring safety of Rust programs, that means avoiding any runtime errors by fixing it right now, like if something is read now and used later like a variable, this could cause a "undefined behaviour" which rust gives out error on, rust ensures memory safety by avoiding this undefine behaviour and catching them which compiling, unlike runtime languages like javascript or python, where the compiler once or twice may run the faulty code but this may left unnoticed and the may cause issues for the user after deployment

Second, we learned that variables live in a frame and there could be multiple frames in a stack, a frame is just like a variable -> value
now to store data in heap we use **Box**
```rust
let a = Box::new([0; 1_000_000]);
let b = a;
```
when we do this a gets copied onto b, but another thing happens, that is ownership of this box is transferred to b
Rust also doesnt let the user manage memory as that can lead to memory issues, like a user frees memory of a variable and tries to use it later

```rust
fn main() {
    let a_num = 4;
    make_and_drop();
}

fn make_and_drop() {
    let a_box = Box::new(5);
}
```
here initially a_num -> 4 is stored in stack, when function is called a_box -> heap(5), and then when function is over, rust deallocates this function and the variables inside and in the stack, only a_num -> 4 remains

```rust
fn main() {
    let first = String::from("Ferris");
    let full = add_suffix(first);
    println!("{full}");
}

fn add_suffix(mut name: String) -> String {
    name.push_str(" Jr.");
    name
}
```

here, initially first -> heap("ferris"), then full calls function add_suffix, now name owns the contents of first since this is not a reference it actually gives the ownership to name, so now first has now way to access this memory, name on pushing becomes heap("Ferris Jr")
and returns name, so now this function is finished, rust deaalocates memory and it returns the name string so now full owns this memory space so full -> heap("Ferris Jr.")

Note that: you cant use first now since it points to nowhere, since on ownership transfer it lost it pointer to the memory 

If you wish to avoid losing variables's ownership you can create a clone of the variable like 

```rust
fn main() {
    let first = String::from("Ferris");
    let full = add_suffix(first);
    println!("{full}");
}

fn add_suffix(mut name: String) -> String {
    name.push_str(" Jr.");
    name
}
```

Now comes the most tough part, i only understood 50% of what is being said, 

References and Borrowing!

like in example above the first variable lost its ownership when the function used it as a parameter and the finsihed and memory deallocated, instead we can pass the reference to the variable which stores address to the heap

```rust
fn main() {
    let m1 = String::from("Hello");
    let m2 = String::from("world");
    greet(&m1, &m2); // note the ampersands
    let s = format!("{} {}", m1, m2);
}

fn greet(g1: &String, g2: &String) { // note the ampersands
    println!("{} {}!", g1, g2);
}
```

just pass the parameters when calling the function with a '&' symbol and on type while defining function 

now when this is called, m1 and m2 point to hello and world in heap, and g1 and g2 point to m1 and m2, and on deallocating m1 and m2 are safe 

to define a variable dynamically you can 
```rust
let mut x : Box<i32> = Box::new(1);
```

to store value of this x on a variable you can dereference this pointer, just like in cpp

```rust
let a: i32 = *x; 
*x += 1;

let r1 : &Box<i32> = &x;
let b : i32 = **r1

let r2: &i32 = &*x;
let c : i32 = *r2;
```

a requires a single asterix as it stored deferences value to addres of x, 
b requres two asterix because r1 stores address to x, so on first asterix `*r1 = x`,  and on second asterix we get `**r1 = *x`, and on c we need only one, so r2 points to address to value of x, so it points directly, so c will be single asterix r2

To define Vector in rust 
```rust
let mut v: Vec<i32> = vec![10,20,30];
v.push(4);
```

vector is stored in heap
```cpp
let mut v: Vec<i32> = vec![1, 2, 3];
let num: &i32 = &v[2];
v.push(4);
println!("Third element is {}", *num);
```

now this will lead to error, because what happens is that vector is defined with 3 digits, now what happens is as new elements is added, a new allocation takes place with larger capacity and all elements are copied over and orignal is deallocated from heap, so a new reference is created so the reference num has is invalid hence this is will eald to error 


Moving on to **TypeScript** ->
im following this [Tutorial](https://www.youtube.com/watch?v=665UnOGx3Pg), this a intro to Typescript i require for React, we have so far learned why type safety is important, so basically what we learn in rust, it is very similar, same things like compile time safety ensures no future bugs to solve down the line when production gets big.

In Typescript as the name suggests we define types like 
```rust
let name: string = "Pedro";
let age: number = 34;
let isMarried : boolean = true;
let ages: number[] = [1,2,3,4];
```

Now further we see how we use interface for props, we define it like this 

```ts
interface Props{
	name: string,
	age: number,
	isMarried: boolean;
}

export const Person = (props: Props) => {
	return (
		<div>
			<p> Name: {props.name}</p>
			<p> Age: {props.age}</p>
			<p> isMarried: {props.isMarried}</p>
		</div>
	)
}
```

the benefit to this is if you turn on strict linting in tsconfig, even if you pass wrong data type to component, linting will tell that the data type is wrong, 
![[/post_2.png]]

## 💭 Thoughts

Today was a information dense day, Ownership in Rust is a challenging thing to understand hopefully within few days i will grasp the concept clearly, also i need to stick to me doing 2 questions daily, i have been not been able to do them these couple days


