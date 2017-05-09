# TinyLaunchbury
A simple implementation of John Launchbury's operational semantics for lazy languages.

Based on John Launchbury's paper [A natural semantics for lazy evaluation](https://pdfs.semanticscholar.org/5276/4f0b318fc02a1ab60144bfbbba698a705452.pdf).  

In GHCI, you can use `displayReduce` to trace through the evaluation of expressions:

    *TinyLaunchbury> displayReduce simpleExpr 

     Reducing let: let u = 3 + 2, v = u + 1 in v + v : {}
     |Reducing primitive: v + v : {v -> u + 1, u -> 3 + 2}
     ||Reducing variable: v : {v -> u + 1, u -> 3 + 2}
     |||Reducing primitive: u + 1 : {u -> 3 + 2}
     ||||Reducing variable: u : {u -> 3 + 2}
     |||||Reducing primitive: 3 + 2 : {}
     ||||||Returning constructor: 3 : {}
     ||||||Returning constructor: 2 : {}
     |||||Primitive evaluated to 5
     ||||Rebinding var u to 5
     ||||Returning constructor: 1 : {u -> 5}
     |||Primitive evaluated to 6 
     ||Rebinding var v to 6
     ||Reducing variable: v : {v -> 6, u -> 5}
     |||Returning constructor: 6 : {u -> 5}
     ||Rebinding var v to 6
     |Primitive evaluated to 12
     Ans: 12
