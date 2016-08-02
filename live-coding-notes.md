# open your src/main.rs

```
fn main() {
    println!("Hello, world!");
}
```

# functions are defined with `fn`
# `main` is the function run when you run a binary
# curly braces around the body of the function
# semicolon at the end of the line

# change the string, cargo run
## show how to see the results of what you've changed

```
fn main() {
    println!("Welcome to the guessing game!");
}
```

# create a variable binding, print it out

```
fn main() {
    println!("Welcome to the guessing game!");
    let guess = "pooo";
    println!("You guessed: {}", guess);
}
```

# try to change the variable value
## variable bindings are by default immutable in rust
## our first compiler error!!!

```
fn main() {
    println!("Welcome to the guessing game!");
    let guess = "pooo";
    guess = "blah";
    println!("You guessed: {}", guess);
}
```

# fix it with mut
## show helpful warning - maybe bug?

```
fn main() {
    println!("Welcome to the guessing game!");
    let mut guess = "pooo";
    guess = "blah";
    println!("You guessed: {}", guess);
}
```

# add `use std::io;` to the top, like java's import
## double colon is namespacing

# start `guess` as a new, empty String
## `let mut guess = String::new();`


# instead of changing `guess` to `blah`
# `io::stdin()` gets a handle to your terminal's standard input
# `.read_line(&mut guess) reads a line into `guess`
## &mut means "a mutable reference to guess"
## we'll talk more when we get to ownership

# run this => unused result warning
## `read_line` returns a Result type-- it might fail
## Rust encourages you to handle all your errors

# what can we do if something like stdin fails?
## shrug, let's crash our program!
## `.expect("Failed to read line");`
## with a nice message about where/why we crashed
## prevents us from continuing to run with invalid stuff

# run, yay! it works! high five! -----------------------------

# generate a secret number
## show xkcd
## generating a random number is hard!
## let's go shopping!
## on the internet, on crates.io, for library crates!
## as opposed to the binary crate we're making
## rust's standard library is small, this is GOOD

# open your Cargo.toml
## add `rand = "0.3.14"`
## cargo run - you'll see updating, downloading, compiling
## want to talk semver? after class
## go look at your Cargo.lock file -
## lists all the exact versions of deps & deps' deps
## so you can have repeatable builds

# back to src/main.rs
# add `extern crate rand;` to the top
# `use rand::Rng;`
# `let secret_number = rand::thread_rng().gen_range(1, 101);`
# how do i know this? from reading rand docs
# for now, print out secret number. who can tell me what to type?
# run a few times, verify that it's not 4

# compare the guess to the secret number
## add `use std::cmp::Ordering;` at the top
## have you written a custom comparator in java?

# at end: `match guess.cmp(&secret_number) {`
# match is like a switch but better
# possibilities of the result of cmp:
## `Ordering::Less => println!("Too small!"),`
## `Ordering::Greater => println!("Too big!"),`
## `Ordering::Equal => println!("You win!"),`

# run: error, mismatched type!
## guess is a string
## secret_number is an... underscore
## rust's type inference hasn't figured it out yet
## it's a number type of some sort, not a string

# conversion time!

let guess: u32 = guess.trim().parse()
    .expect("Please type a number!");

## shadowing variable bindings
## type annotation - unsigned (only positive) 32 bit #
## need that because we could parse to lots of stuff, Rust doesn't know
## trim removes spaces at the beginning and end
## parse changes strings into numbers
## this might fail; crash with a nice messsage
## what are some ways this could fail, software testers??

# run it, try entering a not-a-number
## negative number
## decimal number
## spaces before/after
## higher number
## lower number
## right number


# this game kinda sucks. why?
## allow multiple guessing with `loop`
## will this program run forever? why or why not?

# demonstrate getting out of the loop
## is it a bug or a feature????

# stop when we win using `break`

# what else sucks about this game?
## stop showing the guess
## ignore non-numbers with match/continue
```
let guess: u32 = match guess.trim().parse() {
    Ok(num) => num,
    Err(_) => continue,
};
```

# anything else suck?



## try taking one of the match arms out





