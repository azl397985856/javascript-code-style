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

for example, SOD can be apply to both object-oriented and functional programming.
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

```js
// bad
// i don't know what it exactly mean
const flag = true;

// good
const downloaded = true;
const enabled = true;
```


- use pronouceable name

```js
// bad
// also meaningless
const yyyyMMdd;

// good
const today;
```

- use consistent vacabulary

```js
// bad

// file1
function getUserData()
// file2
function fetchUserData()
// file3
function getUserRecord()
// file4
function getUserInfo()

// good

// file1
function getUserInfo()
// file2
function getUserInfo()
// file3
function getUserInfo()
// file4
function getUserInfo()
```

- use seachable name
```js
// bad
for(let i=0;i<5;i++) {
 // ...
}

// good
const COUNT = 5;
for(let i=0;i<COUNT;i++) {
 // ...
}
```
- use explanatory name

```js

// bad
if (!group) {
  return pictureCollect.list;
}
return getListByGroup(group, pictureCollect.list);

// good
const getAllList = list => list;
// const getAllList = R.identity(list)
if (!group) {
  return getAllList(pictureCollect.list);
}
return getListByGroup(group, pictureCollect.list);
```

- avoid unnecessary context
```js
// bad
const phone = {
 phoneOwner: 'lucifer',
 phoneSize: ''
}

// good
const phone = {
 owner: 'lucifer',
 size: ''
}

```
- never lie

> program never lie, but the comments(also the name) could.
#### type

- prefer const
#### control flow
- prefer promise than callback

> async/await is powerfull too.
### branching
- use short-circuiting or default value

```js
// bad
function downloadFile({_filename, _encoding}) {
   let filename = 'untitled.txt';
   let encoding = 'utf-8'
   if (filename) {
    filename = _filename;
   }
   if (encoding) {
    encoding = _encoding;
   }
   // ....
}

// good
function downloadFile({filename = 'untitled.txt', _encoding}) {
   const encoding = _encoding || 'utf-8';
   // ....
}

```

- use Strategy or polymorphism(Open/closed principle)

- use Chain of Responsibility(Open/closed principle)

- split it into diffrent functions(Single responsibility principle)

- encapsulate conditions

```js
// bad
if (number === 0 && (1 / number) === -Infinity)
// good
function isNegativeZero(number) {
   return number === 0 && (1 / number) === -Infinity
}

if (isNegativeZero(number))
```

- avoid negative conditions
### Expression
- prefer iterator than loop
> recursive bahave better under particular cucircumstance。
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

```js
// bad
const logger = console.log.bind(console)
fetch('http://www.test.com')
 .then(notifyUser)
 .catch(logger)
 
// good

fetch('http://www.test.com')
 .then(notifyUser)
 .catch(err => {
  // You can do it all or just pick one
  console.error(err)
  notifyUser(err)
  sendErrToServer(err)
 })

```
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

```js
// bad
// means the date of the today
const yyyyMMdd;

// good
const today;
```
## Stay Scaleable
### enhance



#### Hollywood Principle
I have always admired the cleverness of the name Hollywood Principle. The essence of this principle is “Don’t call me, I’ll call you”. As you know, this is a response you might hear after auditioning for a role in a Hollywood movie. And this is the same concept for the software Hollywood Principle too. The intent is to take care to structure and implement your dependencies wisely.


for example:

```js

import a from '../../a.js'
import b from '../../../b.js'
import a from '../c.js'

function app() {
   return {
    start() {
     a.start();
     b.start();
     c.start();
     console.log('app stared~')
    }
   }
}


```

We write code which directly depends on a,b and c.
When any of them changes its api or location,
you must follow the steps.

```js
var { decorator } = require("./decorator.public.js");

function app({a, b, c}) {
   return {
    start() {
     console.log('app stared~')
    }
   }
}

// enhance
// = IOC + decorator
decorator(app);

```

if we use enhance, which implemented by IoC and decorator.
the dependencies is injected by something which made the app easy to test and scale up.

the decorator may be just like this:

```js
// for simplicity sake
import a from '../../a.js'
import b from '../../../b.js'
import a from '../c.js'

function decorator(app) {
 return app({a, b, c})
}

```

It's quit simple, but totally different.

- app's params telling the truth
- decoupled from dependencies

And we also can change the app's behaivor.

```js
function a() {console.log('a')}
var _a = a;
a = function() {
 _a();
 console.log('hello decorator')
}
a();
// a
// hello decorator

```

more elegant way:

```js
function a() {console.log('a')}
function dec() {onsole.log('hello decorator')}

compose(dec, a)

```

## Abstraction Oriented
The key of software development is to find out the variable and invariable.

Then programming for the invariable part, make the effect of variable things under control.

Also called programming for abstraction.

Compare with traditional Oject Orintend Programming(OOP), Functional Programming(FP) is more superior.
with the help of 'no data style' , aka 'pointfree', you can separate the details from the logic.
So you can leave the details alone, make the logic pure.

Only that can you write reuseable, mantainable and scaleable code.
