# CMUSphinx pronunciation dictionary

[![build](https://gitlab.com/pwoolcoc/cmudict/badges/master/pipeline.svg)](https://gitlab.com/pwoolcoc/cmudict/commits/master) [![Crates.io](https://img.shields.io/crates/v/cmudict.svg)](https://crates.io/crates/cmudict) [![docs.rs](https://docs.rs/cmudict/badge.svg)](https://docs.rs/cmudict)

This is a rust library for getting pronunciations from the [CMUSphinx][1]
pronunciation dictionary.

## Installation

To use in your `rust` project, add the following to your `Cargo.toml`:

```toml,ignore
[dependencies]
cmudict = "0.2"
```

then in your crate root:

```rust,ignore
extern crate cmudict;
```

## Usage

To use the dictionary, you have to get an instance of the `Cmudict`
struct:

```rust,ignore
extern crate cmudict;

use cmudict::Cmudict;

fn main() {
  let dict = Cmudict::new("./path/to/a/cmudict/file").expect("Couldn't make Cmudict");
}
```

If you don't want to pass your own `cmudict` file, you can call
`Cmudict::download` instead, and the library will download a copy of the
dictionary from https://raw.githubusercontent.com/cmusphinx/cmudict/master/cmudict.dict :

```rust,ignore
extern crate cmudict;

use cmudict::Cmudict;

fn main() {
  let dict = Cmudict::download().expect("Couldn't get/make Cmudict");
}
```

You can retrieve the pronunciation for a word like this:

```rust,ignore
extern crate cmudict;

use cmudict::Cmudict;

fn main() {
  let dict = Cmudict::download().expect("Couldn't get/make Cmudict");
  let word = dict.get("apple").unwrap().pronunciation();
  println!("{:?}", word); // &[Symbol::AE(Stress::Primary), Symbol::P, Symbol::AH(Stress::None), Symbol::L]
}
```

[1]: https://github.com/cmusphinx/cmudict
