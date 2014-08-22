# flate2

[![Build Status](https://travis-ci.org/alexcrichton/flate2-rs.svg?branch=master)](https://travis-ci.org/alexcrichton/flate2-rs)

[Documentation](http://alexcrichton.com/flate2-rs/flate2/index.html)

A streaming compression/decompression library for rust with bindings to
[`miniz`](https://code.google.com/p/miniz/)

Supported formats:

* deflate
* zlib
* gzip

```toml
# Cargo.toml
[dependencies.flate2]
git = "https://github.com/alexcrichton/flate2-rs"
```

## Compression

```rust
extern crate flate2;

use std::io::MemWriter;
use flate2::writer::ZlibEncoder;

fn main() {
    let mut e = ZlibEncoder::new(MemWriter::new(), flate2::Default);
    e.write(b"foo");
    e.write(b"bar");
    let compressed_bytes = e.finish();
}
```

## Decompression

```rust
extern crate flate2;

use std::io::BufReader;
use flate2::reader::GzDecoder;

fn main() {
    let mut d = GzDecoder::new(BufReader::new(b"..."));
    println!("{}", d.read_to_str());
}
```