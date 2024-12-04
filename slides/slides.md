------------------------------------------------------------------
marp: true
footer: github.com/tencek/rust-fp
------------------------------------------------------------------

<!-- _footer: "" -->

![bg 50%](./img/ferris.svg)

------------------------------------------------------------------

# Functional Programming in Rust

------------------------------------------------------------------

![bg right:45%](./img/me.jpg)

Pavel Kučera

- C++ developer since ~2006
- C#/.NET developer since ~2015
- Fan of FP since ~2018 (F#)
- Fan of Rust since 2023

------------------------------------------------------------------

<!-- paginate: true -->

What Rust looks like from the FP point of view. What I was looking for, what I have found, what I am missing.

------------------------------------------------------------------

## What is Functional Programming?

- Function is a basic building block
- Function is a "first class citizen" so a function can be
  - called (obviously)
  - assigned to a variable / expression and call by name
  - passed as an argument
  - returned from another function
  - composed
  
------------------------------------------------------------------

## What is a Function?

```text
      +-------+
      |       |
x --> |   F   | --> y 
      |       |
      +-------+
```

- A "box"
- Single input, Single output
- Every input produces an output (**totality**)
- Same input => same output (**stateless**)
- No side effects (**immutability**)

Quite an limitation! (For good reasons, FPs believe)

------------------------------------------------------------------

```text
      +---+
x --> | F | --> y
      +---+
```

```text
      +---+     +---+
x --> | F | --> | G | --> y
      +---+     +---+
```

```text
         +---+
    +--> | F | --+
    |    +---+   |
x --|            |--> y
    |    +---+   |
    +--> | G | --+
         +---+
```

------------------------------------------------------------------

```text
          +-------+
+---+     |       |
| F | --> |   G   | --> y 
+---+     |       |
          +-------+
```

```text
      +-------+      
      |       |     +---+
x --> |   F   | --> | G | 
      |       |     +---+
      +-------+      
```

```text
          +-------+      
+---+     |       |     +---+
| F | --> |   G   | --> | H | 
+---+     |       |     +---+
          +-------+      
```


------------------------------------------------------------------

## 01 - `let`

- **Nechť** (Czech for "let")
- Originates from LISP
- Resembles mathematics
- Expressions over statements
- Alternatives in other languages: `var`, `Dim`, `def`, `set`, `my`
  - `let` is a good choice

------------------------------------------------------------------

## 01 - `let`

```rust
#[test]
fn test_coffee_machine() {
    let coffee_machine = CoffeeMachine::from(CoffeeMachineSettings::default());
    let coffee_machine = coffee_machine.with_small_size();
    let coffee_machine = coffee_machine.with_max_strength();

    let coffee = coffee_machine.brew();
    assert!(coffee.is_ok());

    let coffee = coffee.unwrap();
    assert_eq!(coffee.water_ml, 30);
    assert_eq!(coffee.caffeine_mg, 40);
}
```

------------------------------------------------------------------

## 01 - `let`

### Summary

💚 Rust looks quite FP-like.

[demo_01_let.rs](https://github.com/tencek/rust-fp/tree/main/demos/src)

------------------------------------------------------------------

## 02 - partial (non-total) functions

### Recap

- Every input produces an output (**totality**)
- What if not? 
- Partial function == undefined behavior

### Example

```rust
// Undefined behavior if bean_weight_mg == 0
pub fn count_beans(portion_weight_mg: i32, bean_weight_mg: i32) -> i32 {
    portion_weight_mg / bean_weight_mg
}
```

------------------------------------------------------------------

## 02 - partial (non-total) functions

 - Rust behavior - panics
 - many languages (F# included) have some sort of exceptions

### Solution in rust

The only option in Rust is to create a total function instead:

```rust
pub fn count_beans(portion_weight_mg: i32, bean_weight_mg: i32) -> Option<i32> {
    portion_weight_mg.checked_div(bean_weight_mg)
}
```

- Client code is forced to check the returned `Option`
- The `checked_div` is a Rust `std` function. There are others as well for intiger overflow, string parse, etc.

------------------------------------------------------------------

## 02 - partial (non-total) functions

### Summary

💚 Rust is great. Even better than e.g. F#

[demo_02_partial_fn.rs](https://github.com/tencek/rust-fp/tree/main/demos/src)

------------------------------------------------------------------

💚💛🧡💔
