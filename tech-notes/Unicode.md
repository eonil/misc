Unicode
=======
Eonil, 2018




Surrogate Pair
--------------
This is a special workaround to solve limited code point space in UTF-16.
This code point won't be used in UTF-8 and UTF-32. These code points shoud
not be appeared in UTF-8 and UTF-32 encoded strings.

In contrast, *Unicode Scalar Values* is all code points except these surrogate
pairs.

In my opinion, 

- **UTF-16 is deprecated**. Tech politics around big corporates is the only reason
  UTF-16 has not been formaly deprecated yet.
- Therefore, *Surrogate Pairs* are also deprecated.
- You should not use Surrogate Pairs.
- Unicode committee defined a new term *Unicode Scalar Values*. Which is actually
  just Unicode Code Points excepting Surrogate Pairs.
- Which means *Unicode Scalar Values* are a newer version of *Unicode Code Point*.
- You should not use concept of *Unicode Code Point* unless you're dealing with
  UTF-16.
- You should use concept of *Unicode Scalar Values* always.
- Even if you're dealing with UTF-16, using of *Unicode Code Point* must be limited
  to encoding/decoding process, and after decoding, you should get and use only
  *Unicdoe Scalar Values* only.

This is so furstrating that it's so hard to find committe's **intention**. Maybe
formal members would access to the intention easily or they have some implicit
and hidden agreement inside. I hate this situation.
