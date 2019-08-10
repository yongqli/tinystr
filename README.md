# tinystr [![Build Status](https://travis-ci.org/zbraniecki/tinystr.svg?branch=master)](https://travis-ci.org/zbraniecki/tinystr) [![Coverage Status](https://coveralls.io/repos/github/zbraniecki/tinystr/badge.svg?branch=master)](https://coveralls.io/github/zbraniecki/tinystr?branch=master)

`tinystr` is a small ASCII-only bounded length string representation.

Usage
-----

```rust
use tinystr::{TinyStr4, TinyStr8};

fn main() {
  let s1: TinyStr4 = "tEsT".parse()
      .expect("Failed to parse.");

  assert_eq!(s1, "tEsT");
  assert_eq!(s1.to_ascii_uppercase(), "TEST");
  assert_eq!(s1.to_ascii_lowercase(), "test");
  assert_eq!(s1.to_ascii_titlecase(), "Test");
  assert_eq!(s1.is_ascii_alphanumeric(), true);

  let s2: TinyStr8 = "New York".parse()
      .expect("Failed to parse.");

  assert_eq!(s2, "New York");
  assert_eq!(s2.to_ascii_uppercase(), "NEW YORK");
  assert_eq!(s2.to_ascii_lowercase(), "new york");
  assert_eq!(s2.is_ascii_alphanumeric(), false);
}
```

Details
-------

It provides two structs:
 * `TinyStr4` an ASCII-only string limited to 4 characters.
 * `TinyStr4` an ASCII-only string limited to 8 characters.

It performs a very tailored set of operations
 * to_ascii_lowercase
 * to_ascii_uppercase
 * to_ascii_titlecase (TinyStr4 only)
 * is_ascii_alphanumeric

This set is sufficient for certain classes of uses such as `unic-langid` libraries.

Performance
-----------

For those uses, TinyStr provides performance superior to regular `String`:

###### FromStr

* 4 char max:
  * String: 1.0779 us
  * TinyStr4: 47.836 ns
  * TinyStr8: 127.37 ns
* 8 char max:
  * String: 1.0864 us
  * TinyStr8: 130.99 ns

###### to_ascii_lowercase

* 4 char max:
  * String: 1.1313 us
  * TinyStr4: 20.164 ns
  * TinyStr8: 28.205 ns
* 8 char max:
  * String: 1.1442 us
  * TinyStr8: 28.211 ns

###### to_ascii_uppercase

* 4 char max:
  * String: 1.1282 us
  * TinyStr4: 20.982 ns
  * TinyStr8: 24.347 ns
* 8 char max:
  * String: 1.1420 us
  * TinyStr8: 24.327 ns

###### to_ascii_titlecase

* 4 char max:
  * String: 1.1487 us
  * TinyStr4: 24.566 ns

###### is_ascii_alphanumeric

* 4 char max:
  * String: 35.767 ns
  * TinyStr4: 21.027 ns
  * TinyStr8: 32.094 ns
* 8 char max:
  * String: 45.881 ns
  * TinyStr8: 32.094 ns

Performance has been tested on MacBook Pro 2017, using Rust 1.36 and tinystr 0.1.0.

Status
------

The crate is fully functional and ready to be used in production.
The capabilities can be extended.

#### License

<sup>
Licensed under either of <a href="LICENSE-APACHE">Apache License, Version
2.0</a> or <a href="LICENSE-MIT">MIT license</a> at your option.
</sup>

<br>

<sub>
Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in Serde by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.
</sub>