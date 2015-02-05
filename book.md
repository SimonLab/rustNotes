# Intro

Notes from the Rust book. Allow to remember the main ideas and concept

# Basics

name with ! at the end are macros: println!(...)
What is a macro in rust? Metaprogramming is done with macro in rustl
Rust is an expression oriented language and most of the things are
expressions. The ; mean the end of an expression.

## Cargo

A Cabal-like.

* Building your code
* Downloading the dependencies for your code
* Building those dependencies

To use cargo to build your code:
* create a configuration file Cargo.toml
* Put the source file to the right place (src)

the Cargo.toml file, two tables:
* package, for the description and metadata about your package
* Bin to indicate to build a binary, not a library

We can build with "cargo build" and run "./target/hello_world"
Cargo.lock is created and track your dependencies needed

## Variables Binding

Rust is statically typed but has type inference
In Haskell :: is for declaring the type
In Rust it's just :
By default binding are immutable
Binding must be initialized

let (x,y) = (1,2) variable can use pattern matching
let x: i32 = 5; x is binding with the type i32 and the value 

To have a mutable binding we can use the tag mut

let mut x = 5;
x = 10;

The code above will compile
The moustache {} can be use for String interpolation
println!("This is a text {}", binding);
The {} try to convert from the type of the binding to a string to
display

## If

if come from the concept of the branch
if x == 2 {
println!("some value");
}else{
println! ("other value");
}

We can bind the expression of the if to a variable
let y = if x == 5 {10}else{15};

### Expressions vs Statements

Expressions return a value, the statements don't.
There are only two statements in rust
binding is one of them and it's called declaration statement
let x = value; doesn't return a value

In Ruby we can use expression for binding

x = y = 5 works with ruby

assigning to an existant value is an expression!

The second statement is called expression statement. Its goal is to
turn every expression into a statement. We use the ; to transform an
expression into a statement. In this case the return value is deleted
and rust use the unit () instead (because a statement doesn't return
any value).

let y: int32 = if x == 3 {10;}else{15;} won't compile because y except
a int32 but 10; or 15; return now a unit ()

## Functions

fn main() {},  fn allow to define function

A fuction declaration with an argument. We nust declare the type of
the argument
fn  print_number(x: i32) {
  println! ("the value of x is {}, x);
  }

A function which returns a value
fn add_numbers(x: i32, y: i32) -> i32{
  x + Y
}

We can use return for an early return
fn foo(x: i32) -> i32 {
    if x < 5 { return x; }

    return x + 1;
}

## Comments
// line comments
/// doc comments and support markdown
we can use rustdoc to generate the doc

## Compouds data Type

### Tuples

let x: (i32,&str)  = (1, "hello");

With pattern matching
let (x,y,z) = (1,2,3);
println!("the value of x is {}", x);

We can assign a tuple if it's the same type
let mut x = (1,2);
let y = (2,3);
x =y;

We can compare tuples with ==
We can simulate to return multiple value with a tuple
fn next_two(x: i32){
  (x+1,x+2)
  }

### Structs

struct is a form of record type. The struct type create fields (or
member) for each element of the struct

struct Point{
x: i32;
y: i32;
}

fn main(){
let origin = Point{x:0,Y:0};
println!("origin x {}, y {}", origin.x, origin.y);
}

The name of a struct begin with a capital letter and use camelCase
We create as usual an instance of the struct with let but we define
the inside value with key: value.

The elements of a struct have names so we can call them with the dot
notation
origin.x

The values are immutable by default, use mut on the instance of the
struct to be able to change the value.

let mut s = Point{...}
s.x = 56;

### Tuple Structs and newtype

tuple struct have name but their values don't

struct Color(i32,i32,i32);
struct Point(i32,i32,i32);

Color and Point are not equal, they represent different objects.
It's almost always better to use struct instead of tuple struct.

newtype is a tuple struct with just one value
struct Inches(i32);

### Enums

enum Ordering {
    Less,
    Equal,
    Greater,
	}

Every varient of the enum is namespaced	
We access the values of the enum with ::
Ordering::Less. :: is used to access a namespace

enum OptionalInt {
    Value(i32),
    Missing,
	}

It looks like the Maybe of Haskell

use StringResult::StringOK;
use StringResult::ErrorReason;

enum StringResult {
    StringOK(String),
    ErrorReason(String),
}


fn respond(greeting: &str) -> StringResult {
    if greeting == "Hello" {
        StringOK("Good morning!".to_string())
    } else {
        ErrorReason("I didn't understand you!".to_string())
    }
	}

## Match
