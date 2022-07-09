# Rust
Rust is a [[Computer Science|programming language]] created by Mozilla. It was developed as a replacement to [[C++]], which is extremely performant, but is notorious for producing programs which mismanage system memory.

## Concurrency in Rust
Futures in Rust are lazy. By default, they won’t do anything before they’re polled the first time. The future gets polled when you `await` it.

## HIR
HIR stands for "High-Level Intermediate Representation". It is a compiler-friendly representation of the abstract syntax tree (AST) that is generated after parsing, macro expansion, and name resolution.

## MIR
MIR is Rust's _Mid-level Intermediate Representation_.

## Rust Dev Guide
The [Rust Dev Guide](https://rustc-dev-guide.rust-lang.org/contributing.html) is a great place to read about the internal workings of the language.

## Release Build Optimizations
```
[profile.release]
codegen-units = 1 # Removes dead code
opt-level = "s" # Optimize for size
lto = true
```

See [Min Sized Rust](https://github.com/johnthagen/min-sized-rust) for a list of tricks to improve your build size!