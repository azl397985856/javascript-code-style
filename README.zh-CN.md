# javascript-code-style
这篇报告包含了几乎所有关于写好代码的内容，尤其是在构建大型应用程序时。

主要包括四个部分:

- 基本原则

- 保持整洁

- 保持扩展性

- 抽象化

> 本主题仅涉及原生js，关于框架（比如react和vue）的内容会在以后的文章中展现。

## 基本原则
我想你们大多数人之前都听说过SOLID，也就是面向对象设计里的SOLID原则。

这些原则基于面向对象设计，所以可能不适合其他编程形式。即便如此，它也涵盖了大多数情况。

例如，SOD既可以应用于面向对象编程，也可以应用于函数式编程。
### 单一责任原则（SRP）
### 开放封闭原则（OCP）
### 里氏替换原则（LSP）
### 接口分离原则（ISP）
### 依赖倒置原则（DIP）
## 保持整洁
### 变量
变量可能是在开发过程中最常见的术语。
#### 命名
- 使用语义明确的命名

```js
// 不推荐
// 我不知道这个变量代表什么意义
const flag = true;

// 推荐
const downloaded = true;
const enabled = true;
```


- 使用被人熟知的命名

```js
// 不推荐
// 也是没有意义
const yyyyMMdd;

// 推荐
const today;
```

- 使用语义一致的词汇

```js
// 不推荐

// file1
function getUserData()
// file2
function fetchUserData()
// file3
function getUserRecord()
// file4
function getUserInfo()

// 推荐

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
// 不推荐
for(let i=0;i<5;i++) {
 // ...
}

// 推荐
const COUNT = 5;
for(let i=0;i<COUNT;i++) {
 // ...
}
```
- use explanatory name

```js

// 不推荐
if (!group) {
  return pictureCollect.list;
}
return getListByGroup(group, pictureCollect.list);

// 推荐
const getAllList = list => list;
// const getAllList = R.identity(list)
if (!group) {
  return getAllList(pictureCollect.list);
}
return getListByGroup(group, pictureCollect.list);
```

- 避免冗余的命名
```js
// 不推荐
const phone = {
 phoneOwner: 'lucifer',
 phoneSize: ''
}

// 推荐
const phone = {
 owner: 'lucifer',
 size: ''
}

```
- 永远不要说谎

> 程序从不说谎，但注释（也包括名称）可能会。
#### 类型

- 使用 const
#### 控制流
- 使用promise方法而不是callback（回调函数）

> 异步/等待也是强大的。
### 分支
- 使用短路表达式或默认值

```js
// 不推荐
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

// 推荐
function downloadFile({filename = 'untitled.txt', _encoding}) {
   const encoding = _encoding || 'utf-8';
   // ....
}

```

- 使用策略或多态性（开放封闭原则）

- 使用责任链（开放封闭原则）

- 将其分解成不同的功能（单一责任原则）

- 封装条件

```js
// 不推荐
if (number === 0 && (1 / number) === -Infinity)
// 推荐
function isNegativeZero(number) {
   return number === 0 && (1 / number) === -Infinity
}

if (isNegativeZero(number))
```

- 避免不必要的条件
### 表达
- 使用迭代器而不是循环
> 在特定环境下递归表现的更好。
### 函数
#### 参数尽量要少
#### 使用纯函数
#### 相比于命令式，函数式更好
#### 小心在全局作用域中的函数（包括在他们原型对象上的方法）
#### one level of abstraction
#### 只做一件事情（单一责任原则）
#### write less
#### 调用者和被调用者位置应该尽量接近
### 报错
- 不要对报错不做处理

```js
// 不推荐
const logger = console.log.bind(console)
fetch('http://www.test.com')
 .then(notifyUser)
 .catch(logger)
 
// 推荐

fetch('http://www.test.com')
 .then(notifyUser)
 .catch(err => {
  // 你可以全做，也可以选一个
  console.error(err)
  notifyUser(err)
  sendErrToServer(err)
 })

```
> 打印、存储、通知用户或将其发送到远程服务器
### 测试
- 一步一测试
### 格式
- 美观

- 一致

### 注释
- 注释让人难以理解的关键部分

- 删除注释代码

- 注释必要的信息

> create, ltime etc

- 避免绘图注释

- 根据代码意义注释，不要说谎

- 注释应与相关代码位置一致

- 相比于注释，一个语义明确的命名更好

```js
// 不推荐
// means the date of the today
const yyyyMMdd;

// 推荐
const today;
```
## 保持扩展性
### enhance



#### 好莱坞原则
我一直很欣赏好莱坞原则这个名称的巧妙。这个原则的本质是“不要给我打电话，我会打给你”。如你所知，这是你在面试好莱坞电影里的一个角色后可能听到的答复。而软件世界里的好莱坞原则也是一样的观念。其目的是注意要聪明的构造和实现你的依赖关系。


例如:

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

我们编写的代码直接依赖于a、b和c。当它们中的任何一个改变它的api或位置时，你必须跟着变动代码。

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
依赖项被注入了一些东西，使得应用程序易于测试和扩展。.

装饰器可能就像这样：

```js
// 为了简单的目的
import a from '../../a.js'
import b from '../../../b.js'
import a from '../c.js'

function decorator(app) {
 return app({a, b, c})
}

```

这很简单，但完全不同。

- app的参数道出了真相
- 从依赖项中解耦

而且我们可以改变app的行为.

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

更优雅的方式：

```js
function a() {console.log('a')}
function dec() {onsole.log('hello decorator')}

compose(dec, a)

```

## 抽象化
软件开发的关键是找出变量和变量。

然后对不变部分进行编程，使变量的影响在它的控制之下。

也称为抽象编程.

对比传统的面向对象编程（OOP）来说,函数式编程（FP）更优越。
借助“无数据样式”（即“pointfree”）的帮助，您可以将细节与逻辑分离开来。
所以你可以单独留下细节，让逻辑变得纯粹。

> 我想再强调一点，那就是人们有时会说，没有抽象概念总比错误的抽象好。这实际上意味着错误抽象的代价非常高，所以要小心。我认为这有时会被误解。这并不意味着您应该没有抽象概念。 **这只意味着你必须非常小心。**     --  Malte Ubl在JSConf澳大利亚演讲。

我们必须善于发现正确的抽象。

只有这样，您才能编写可重用的、可管理的和可扩展的代码。

