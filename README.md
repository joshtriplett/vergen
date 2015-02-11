# vergen
Includes 3 functions for use in version strings in ```lib.rs/main.rs``` at compile time via a custom cargo build script.

```rust
pub fn now() -> &'static str {
   // Output of 'date --frc-3339=ns'
}

pub fn sha() -> &'static str {
   // Output of 'git rev-parse HEAD'
}

pub fn semver() -> &'static str {
   // output of 'git describe
}
```

## Basic Usage
#### Cargo.toml
```toml
[package]
#
build = "build.rs"
#
[build-dependencies]
vergen = "*"
```
#### build.rs
```rust
use vergen::vergen;

fn main() {
    vergen();
}
```
#### lib.rs/main.rs
```rust
include!(concat!(env!("OUT_DIR"), "/version.rs"));

// The following is an exmaple.  You could use now(), sha(), and semver() however you want.
fn version() -> String {
    format!("{} {} {}", now(), sha(), semver())
    // 2015-02-11 15:35:30.991638113-05:00 b8acdc17bbf0d9928f08b15cba6d3b659770a624 rh v0.0.1-pre-21-gb8acdc1
}
```