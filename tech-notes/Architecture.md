Architecture
============
Hoon H.

When you write an app, just follow MVC pattern, and it's usually 
just fine. But there's a pitfall. 

Re-enterring Problem
--------------------
Normally, MVC pattern require view to observe model.
In Apple MVC, view-controller observes model.
This makes you to write model event handlers.
And for whatever reason, you MUST NOT modify model again
in those event handlers. Because it will make your execution
context to re-enter into the model mutation function, 
and it can yield subtle and delayed (which hides source of bug) 
crash.

This rule can be forgetten very easily, but VERY IMPORTANT.
Because if you re-enter into model mutator by mistake, such
mistake is very hard to catch, and also hard to fix.

So I have to explan this more.

Let's assume you have a model and two views.

    class Model {
        var items = [String]()
        func appendNew() {
            // Mutate state.
            items.append("AAA")
            // Dispatch event to observing views.
            renderView1(.insert(index: 0))
            renderView2(.insert(index: 0))
        }
        func deleteLast() {
            // Mutate state.
            items.removeLast()
            // Dispatch event to observing views.
            renderView1(.delete(index: 0))
            renderView2(.delete(index: 0))
        }
    }
    enum Event {
        case insert(index: Int)
        case delete(index: Int)
    }

It looks fine here. But what if an observer try to mutate 
model while handling an event?

    func getModel() -> Model { ... }
    func renderView1(e: Event) {
        switch e {
        case .insert(let index):
            let item = getModel().items[index]
            // Do some rendering...
            // BAD CODE HERE!!!
            getModel().deleteLast()
        case .delete(let index):
            ...
        }
    }
    func renderView2(e: Event) {
        switch e {
        case .insert(let index):
            // What would happen here?
            let item = getModel().items[index] 
            // Do some rendering...
        case .delete(let index):
            ...
        }
    }

`deleteLast()` call will be executed BEFORE `renderView2()`
to be called. When `renderView2()` is getting called, there's
no item, so the code will crash.

You MUST keep state unchanged while it is being broadcasted
to all observers. You MUST keep the event to describe mutation
properly. 

There's no easy way to deal with this. You just care not to
re-enter to model mutator. Whatever you touch, it will become
disaster if you mutate model AGAIN in event broadcasting.



Local Copy
---------- 
Not always, but usually views or view-controllers need to
keep local copy of some model data to get old state. Because
model event sent after every mutation has been done, so 
usually there's no way to get old state. Well you can carry
some of old state as a part of event data, but keeping a 
local copy is actually better in many ways.



Coroutine Continuations
-----------------------
Models can perform asynchronous operation and return a future 
object as a continuation point. This future will continue
just right after all the event dispatches are done. Now the 
continuation point is perfectly safe to execute next operation
or even call another asynchronous model operation.

So this is, 

    * Mutate
    | 
    * Dispatch event to all observers
    |
    * Continue future.

NEVER mutate a state between event dispatch and future 
continuation.










State Consistency
-----------------







Apple MVC
---------
In Apple's MVC, you just need view-controller to observe model, 
and translate model events into view commands. It could feel a
bit bloated, or making view-controller somewhat fat, but 
actually, this is the best way to DE-COUPLE model and view.
Please make sure that your view NEVER depend on any model or 
controller component. Because it will make hard-coupling between
your view and model, and maintenence-ability and re-usability 
becomes hell.






Copying vs Timing
-----------------
There're two approaches on overall architecture.

> Copying vs Timing

You can copy your model state over time, keep them in a queue
and send them to views. This is more functional, needs less
care, but you lose many traditional stack based debugging 
opportunities because this is essentially asynchronous operations.

Otherwise, you need to do everything in PRECISE timing. In this
traditional imperative style, it's uaully easier to debug with 
stacks, but it could be hard to be precise. 

Anyway, I would recommend latter one becuase it's easier to debug.
Also I think we can provide some dynamic checks to catch out
programmer errors.








Application vs Simulation
-------------------------
Such timing based architecture is just an optimized architecture 
for applications. Applications usually does not mutate very 
frequently, so it's usually easy to track over call-stack.

But in simulations, mutations are very frequent (like for each tick)
and call-stacks usually doesn't help a lot for debugging. In this 
situation, it's better to keep stream of state history, and mutation
logs. So in such simulation programs, I recommend to try copy based
architecture. Anyway, this has not been tried much by myself.






















