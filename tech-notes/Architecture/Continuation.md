Architecture/Continuation
=========================
2016/10/27
Hoon H.

What is *continuation*? I don't know either well, but I can explain a bit.

Just imagine that you have a function which can be paused and resumed
in the middle of execution. If you want to resume a paused function, then
you need a *pointer* which indicates where to resume. Not just a position,
but also you need accumulated execution state to the point.

The pointer is a continuation.

Simulations. Games.
===================
Why do you need a continuation? Because it simplifies many thing a lot
simpler. A significant example is coroutine. You can have multiple 
execution context using continuation. Actually, continuation can be
created easily by dividing part of execution into multiple closures,
and it's typical, and nothing special nowadays.

But that's not enough. I mean for simulations. Specifically, for games.

What I need is *serialization of that continuation*. And persisting and 
restoring the continuation.

Nowadays, almost all languages support closures. And some of them support
first class continuation. But almost none of them support serialization
of continuation. So far, the only language I know is Smalltalk.



Emulating Reliably Persistable Continuations
--------------------------------------------
As I said before, it's easy to make a continuation. But it's not easy to 
serialize a continuation. To make it serializable, you need to make every
execution states transparently serializable. Also, you need to track position
of executed program.

Moreover, if you need to make serialization reliable, portable across the 
platforms, you need to keep original program structure as is. Which means no opportunity for any kind of optimization.












