# ConstDefault Trait

[![Crates.io](https://img.shields.io/crates/v/constdefault)](https://crates.io/crates/constdefault) [![Crates.io](https://img.shields.io/crates/l/constdefault)](LICENSE) [![docs.rs](https://img.shields.io/docsrs/constdefault)](https://docs.rs/constdefault) [![actions](https://github.com/AerialX/constdefault.rs/actions/workflows/rust.yml/badge.svg)](https://github.com/AerialX/constdefault.rs/actions/workflows/rust.yml)

A `Default`-like trait and derive macros for `const` evaluation contexts.

This crate defines the `ConstDefault` trait and implements it for
Rust primitives, prelude types, tuples and arrays. Furthermore it
provides a derive macro so that users can implement `ConstDefault`
easily for their custom types.

- 100% safe Rust
- `no_std` compatible
- Full macro hygiene
- No dependencies

## Usage

Add
```toml
[dependencies]
constdefault = { version = "1.0", features = ["derive"] }
```
to your `Cargo.toml` to start using it.

## Examples

### Rust Primitives

```rust
use constdefault::ConstDefault;

fn main() {
    assert_eq!(<i32 as ConstDefault>::DEFAULT, 0);
    assert_eq!(<Option<i32> as ConstDefault>::DEFAULT, None);
    assert_eq!(<String as ConstDefault>::DEFAULT, String::new());
    assert_eq!(<Vec<u8> as ConstDefault>::DEFAULT, Vec::new());
}
```

### Derive

```rust
use constdefault::ConstDefault;

#[derive(ConstDefault, Debug, Default, PartialEq)]
pub struct Color {
    r: u8,
    g: u8,
    b: u8,
}

fn main() {
    assert_eq!(
        <Color as ConstDefault>::DEFAULT,
        Color::default(),
    );
}
```
