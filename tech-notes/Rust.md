Rust
====
Hoon H.

Points
------
- `str` is a slice of `String`.
- `String` carried its ownership, and `str` doesn't.
- Each source file (`.rs`) becomes a module implcitly.
    To use features in another file, you need to import
    it explicitly like this.

        mod Sample1;
        use Sample1::*;


