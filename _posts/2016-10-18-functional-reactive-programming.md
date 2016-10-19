---
layout: post
title: Functional Reactive Programming
data: 2016-10-18
--- 
## FRP
Funtional Reactive Programming (FRP) is a library that replaces listers (callbacks) in the observer pattern for clearer and simpler code. It is about refactoring  specific area of code that focuses on event propogation. FRP is a replacement for the observer pattern i. e. event  listeners and callbacks. One of the main goals of FRP is to bring order to the management of state. 

The term “reactive” refers to inputs or the flow of data. It is event based, acting in response to input, and focuses on the flow of data rather than the flow of control. 

Reactivity is fused with "Functional" in the form of compositionality from Functional Programming.

The Rx library is also reactive in that it chains event handlers. But FRP's addition of functional programming brings a tighter control to your codebase.

### Manning Book
_Functional Reactive Programming_ (Manning, 2016) describes two ways to architect appications. The first is through threads, which refers to control flow. This is good for I/O and a clearly defined sequence (e.g through Actors and generators). Threads express control through sequences. The seond way is through Events. This refers to discrete and asynchronous messages. Think GUIs and videogames. Events express control through dependencies. Both of these methods manage state change via inputs. A problem arises when the way these two methods switch how they express control. Programming is basically organizing and controlling state machines, or when apps change state to logic. Confuse the logic, and you've got trouble.

### LIstener Plagues
The author describes the six plagues of listeners:
- Unpredictable orders- Events depend on listener order
- Missed first event- Hard to know if listener is registered
- Messy state- Callbacks force state-machine style
- Threading- Hard to know if the listener won’t have more callbacks
- Leaking callbacks- If listeners aren’t closed, program leaks memory
- Accidental recursion- Order of state and listeners matter

There are a few ways to isolate and manage state. Instead of variables, the author suggests using cells. Cells are values that change over time. Channel events through streams, or a sequence of events similar to pipes. A stream is an event, an event stream, an observable, a signal. A good way to think of this is a spreasheet. There is a formula with criteria or conditions, and cells linked to one another will change reactively to these formulas. Cells are sources of info, and the only sources of info.

### Reactive Libraries
The author works on a library called Sodium. This is a push-based library similar to RxJS. But RxJS doesn’t deal with simultaneous events so they can’t be FRP. Some FRP is pull-based. FRP is the declarative description of the output in terms of input. As far of Event Handling, in FRP there is always one argument. Could be a unit, a dummy argument with no information. You could also use the “never” stream or a stream that never fires.
Sodium has 10 primities, 2 classes (stream and cell), that both output streams, cells, or values. Primitives are operators or functions that are higher order such as map or filter.

### Testing in FRP
The book closes with an interesting note on testing with functional programming. "To some extent, TDD exists to compensate for the lack of checking that is inherent to imperative programming. In dynamic typed language, TDD is important. FRP basically has TDD baked in. But logic tests are still important with unit tests."

