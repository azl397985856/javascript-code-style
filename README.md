# javascript-code-style
This repo contains almost everything about writtig good code especially when you'r building large apps.

It mainly cover there four parts:

- Basic Princeple

- Keep Clean

- Stay Scaleable

- Abstraction Oriented

> this topic only covers the native js, and the framework parts such as react and vue are on their way.

## Basic Princeple
I think most of you have heared SOLID before,aka SOLID (object-oriented design).

These princeples base on the object-oriented design, 
so maybe itsn't quit suitable for other programming paradigm。
even so, it covers most cases.

for eample, SOD can be apply to both object-oriented and functional programming.
### Single responsibility principle
### Open/closed principle
### Liskov substitution principle
### Interface segregation principle
### Dependency inversion principle
## Keep Clean
### Variable
variable could be the most frequent term during the development.
#### naming
- use meaningful name

> the naming 'flag' is terrible

- use pronouceable name

- use consistent vacabulary

- use seachable name

- use explanatory name

- avoid unnecessary context

- never lie
#### type

- prefer const
#### control flow
- prefer promise than callback

> async/await is powerfull too.
### branching
- use short-circuiting or default value

- use Strategy or polymorphism(Open/closed principle)

- use Chain of Responsibility(Open/closed principle)

- split it into diffrent functions(Single responsibility principle)

- encapsulate conditions

> if (doorKeeper(v))

- avoid negative conditions
### Function
#### prefer fewer arguments
#### prefer pure function
#### prefer functional than imperative
#### be careful about the global functions(include methods on prototype)
#### one level of abstraction
#### only do one thing(Single responsibility principle)
#### write less
#### caller and callee should be close
### Error
- dont't catch error silently
> print , stash, notify the user or send it to remote sever.
### Testing
- single concept per test
### Format
- beatifull

- consistant

### Comment
- comment the key part which is hard to understand

- remove the commented code

- comment the necessary info

> create, ltime etc

- avoid drawing comment

- never lie

- comment should keep up with the relevant code

- prefer meaningfull naming than comment
## Stay Scaleable
### enhance

> Dependency inversion principle


## Abstraction Oriented
The key of software development is to find out the variable and invariable.

Then programming for the invariable part, make the effect of variable things under control.

Also called programming for abstraction.

Only that can you write reuseable, mantainable and scaleable code.
