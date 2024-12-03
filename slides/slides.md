---
marp: true
footer: github.com/tencek/rust-fp
---

<!-- _footer: "" -->

![bg 50%](./img/ferris.svg)

---

# Functional programming in Rust

---

![bg right:45%](./img/me.jpg)

Pavel Kučera

- A C++ developer since ~ 2006
- A C#/.NET developer since ~ 2015
- A fan of FP since ~ 2018 (F#)
- A fan of Rust since 2023

---

## What is Functional Programming

---

## What is a function?

---

<!-- paginate: true -->

## `let`

 - originates from LISP
 - reminds math
 - nechť
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