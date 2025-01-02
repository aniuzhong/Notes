Structured Concurrency
======================

[Wikipedia](https://en.wikipedia.org/wiki/Structured_concurrency)


Journals from ACCU
------------------

[Structured Concurrency in C++](https://accu.org/journals/overload/30/168/teodorescu)

[Senders/Receivers: An Introduction](https://accu.org/journals/overload/32/184/teodorescu)


Topics from Reddit
------------------

[Do you think the current asynchronous models (executors, senders) are too complicated and really we just need channels and coroutines running on a thread pool?](https://www.reddit.com/r/cpp/comments/146e4v3/do_you_think_the_current_asynchronous_models/)

**mjklaim** has the following viewpoints:

- Coroutines does not imply asynchronous models. Whatever asynchronous model exists in a language, coroutine is the syntaxe that helps use it transparently, it's not the model itself.
- Thread pools are just one way to handle concurrency resources, it have nothing to do with how you write algorithms to exploit concurrency resources nor is it the rigth solution for every problem (far from it). It also doesnt tell you how to track the state of tasks or build a task graph (aka, a concurrent program).
- Channels solves exactly one kind of concurrency synchronization (or more like communication), which basically removes you from beeing able to solve most other problems.
- The idea of having a way to pass an object representing the concurrency resources to use to an algorithm is crucial to be able to combine generic algorithms and any concurrency resource available.
- Sender&Receiver(&Scheduler) (aka P2300) mainly provides a common API for the thing that represent an execution resource (scheduler), the thing that represent a task (sender) that knows how to notify the callback receiving it's result (receiver) and allowing senders to also be receivers (more or less) so that you can build a DAG of tasks coming from various libraries to do complex work. Most of the proposal is concepts, which basically means it's setting up a common convention so that other code knows how to manipulate all that without knowing the exact types and libraries being manipulated. The principles are simple, the specification might be complicated, but you only need to get the principles.
- The building blocks are not what most of devs will be exposed to, most of us will simply use libraries using these building blocs and doing whatever we want them to do (you can use your channels and threadpool if you want and that matches your projects). The current proposals are about the building blocks, for those who have to properly handle concurency and make their user's life easier.


P2300 (senders/receivers)
-------------------------

[stdexec](https://github.com/NVIDIA/stdexec)

https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2024/p2300r10.html
