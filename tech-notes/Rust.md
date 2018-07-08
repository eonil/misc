Rust
====
Hoon H.

Points
------
- `str` is a slice of `String`.
- `str` is a primitive type, and `String` is a utility
    which is defined in standard library.
- `String` carried its ownership, and `str` doesn't.
- Each source file (`.rs`) becomes a module implcitly.
    To use features in another file, you need to import
    it explicitly like this.

        mod Sample1;
        use Sample1::*;




When to Use References
----------------------
Move-after-reference is disallowed to prevent logical error.
Because basically it doesn't make sense.
You shouldn't move any value after it's been referenced.
This means, you can't reference an arbitrary values. 
Values can be referenced only as long as they have clear identity.
In other words, once referenced values cannot be moved forever until
all references are removed. This brings limitation on designs.

- *If you want to produce a freely **moveable & copyable** value, you **cannot
  store references** to the value.*

- You can make reference a value only while you can fix the value at a
  single address. 
  
- As a result, in most cases, you can make reference only
  to pass storage address to calculation subprocedures.
  
- If you force to fix a value at an address, it's no more free to
  move or copy. In this case, you may store references.
  But this introduces huge limitations on design. In most cases, 
  what you can freely reference is only immutable values. You can 
  have only one reference to a mutable value, and this is usually
  not storable in long term. It's possible to store such mutable
  reference as a part of temporary struct to keep information
  for short term execution such as a function arguments.
  
- For resource types, you have to allocate them at a certain location,
  and you can't move them forever until it dies.
  
