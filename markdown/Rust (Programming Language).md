# Rust
Rust is a [[Computer Science|programming language]] created by Mozilla. It was developed as a replacement to [[C++]], which is extremely performant, but is notorious for producing programs which mismanage system memory.

## Concurrency in Rust
Futures in Rust are lazy. By default, they won’t do anything before they’re polled the first time. The future gets polled when you `await` it.