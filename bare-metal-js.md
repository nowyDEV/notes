# Notes from [Bare Metal JavaScript](https://frontendmasters.com/courses/javascript-cpu-vm/)

## CPU

- Modern CPUs use [Speculative execution](https://www.extremetech.com/computing/261792-what-is-speculative-execution)
- The CPU clock speed (GHz) and parallel execution tasks limit has been reached, the only thing that's still possible to improve CPU performance is adding more cores
- Some of the cores have slow performance and consume low amount of power, some are very fast and consume way more power. Usually applications run on slow cores, they are being switched to the faster cores when they need to perform expensive tasks
- Because JS runs on a single core, it does not benefit from multiple cores
- There are no good primitives when it comes to paralleization for JS, the cost of using Service Workers is high and the implementation itself might require a great deal of work

## VM inlining & deopt

- Deoptimization - process of the compiler where it reruns the inlined code after it notices inlined entity changes
- Because of inlining and deopting, it's easy to misinterpret results of a microbenchmarks
- In certain cases, we can opt for inlining functions ourselves
- [Deopt Explorer](https://devblogs.microsoft.com/typescript/introducing-deopt-explorer/) analyses traces produced by V8 and helps with performance analysis
- To improve performance of objects, avoid adding properties dynamically - define all of them from the start and set the ones that are not yet defined to "undefined", thanks to that they will have the same hidden class. This relates to avoiding optional properties in TypeScript if possible
- Having the single place (factory function) to allocate the object might be handy
- JSX where objects always have different shape (props) has a pretty bad performance (it doesn't matter that much since DOM is a performance bottleneck anyways)
- Most of the caches can contain 1024 items, when you have an object with more than 1024 properties and you try to read them, you might vastly hinder the performance

## Micro benchmarking

- "===" operator is faster than "==" up to 15 times (no additional coersion required)
- Adding properties on prototype might cause unexpected behavior (this is common knowledge that it should be avoided) - e.g. adding `valueOf` to an object improves performance on "==" operation (coersion of an object is done using valueOf prop)
- Copying objects is way more expensive than copying arrays
- Microbenchmarks might not be reliable for dynamically compiled languages like JS due to inline caching and other optimizations (skipping), complex scenarios reflect reality more closely. It's possible to turn off optimizations through node options (turning off inlining might be useful in some cases)
- Arrays with holes ([1, 2, , 3]) have slower reads, to retrieve index of a "hole" an additional call to prototype chain is made
- V8 has speciall class arrays for different array types (e.g. numbers arrays, floating-point numbers arrays, mixed types arrays, holey arrays). Holey arrays are the worst when it comes to read performance

## Summary

- Write code that's readable and easy to understand for others, stick to some fundamental rules when it comes to performance listed above, optimize where it matters or when there are visible bottlenecks
- Don't mess with prototype
- Avoid performance bottlenecks (Holey arrays, "==" equality operator, copying big objects, adding properties on the fly)
- Use Deopt Explorer to analyze performance
- Be careful with trusting microbenchmarks

## Additional resources

- [Understanding Monomorphism to Improve Your JS Performance up to 60x](https://www.builder.io/blog/monomorphic-javascript)
- [Amdahl's law](https://twitter.com/mhevery/status/1626722915550117888)
- [Performance tips for JavaScript in V8](https://web.dev/articles/speed-v8)
