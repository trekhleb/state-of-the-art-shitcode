# 垃圾代码书写准则

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

这是你的项目应该遵循的一个垃圾代码书写准则的列，把称为适当的垃圾代码。

_Read this in other languages:_
[_English_](https://github.com/trekhleb/state-of-the-art-shitcode)

## 获取徽章

如果你的仓库遵循垃圾代码书写准则，你应该用下面的"state-of-the-art shitcode" 徽章：

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

标记徽章的源代码:

```
[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)
```

## 准则

### 💩 打字越少越好

以一种代码已经被混淆的方式命名变量，如果我们键入的东西越少，那么就有越多的时间去思考代码逻辑等问题。

_Good 👍🏻_

```javascript
let a = 42;
```

_Bad 👎🏻_

```javascript
let age = 42;
```

### 💩 变量/函数混合命名风格

我们需要混合命名方法与变量，这样才能体现命名的多样性。

_Good 👍🏻_

```javascript
let wWidth = 640;
let w_height = 480;
```

_Bad 👎🏻_

```javascript
let windowWidth = 640;
let windowHeight = 480;
```

### 💩 不要写注释

反正代码都看得懂，为什么要写注释？或者说，反正没人看我的代码，为什么要写注释？

_Good 👍🏻_

```javascript
const cdr = 700;
```

_Bad 👎🏻_

更多时候，评论应该包含一些“为什么”，而不是一些“是什么”。如果“什么”在代码中不清楚，那么代码可能太混乱了。

```javascript
// 700ms的数量是根据UX A/B测试结果进行经验计算的。
// @查看: <详细解释700的一个链接>
const callbackDebounceRate = 700;
```

### 💩 使用母语写注释

如果您违反了“无注释”原则，那么至少尝试用一种不同于您用来编写代码的语言来编写注释。如果你的母语是英语，你可能会违反这个原则。既然编程语言绝大多数都是用英文，那么为什么不用其它语言注释一下？

_Good 👍🏻_

```javascript
// 隐藏错误弹窗
toggleModal(false);
```

_Bad 👎🏻_

```javascript
// Hide modal window on error.
toggleModal(false);
```

### 💩 尽可能混合不同的格式

为不同庆祝一下。同样，为了代码的多样性，我们需要尽可能混合不同的格式，例如单引号或双引号。如果它们的语义相同，那就应该混用。

_Good 👍🏻_

```javascript
let i = ['tomato', 'onion', 'mushrooms'];
let d = [ "ketchup", "mayonnaise" ];
```

_Bad 👎🏻_

```javascript
let ingredients = ['tomato', 'onion', 'mushrooms'];
let dressings = ['ketchup', 'mayonnaise'];
```

### 💩 尽可能把代码写成一行

如果一系列参数与方法都是一起实现的，那么代码也要写在一起。

_Good 👍🏻_

```javascript
document.location.search.replace(/(^\?)/,'').split('&').reduce(function(o,n){n=n.split('=');o[n[0]]=n[1];return o},{})
```

_Bad 👎🏻_

```javascript
document.location.search
  .replace(/(^\?)/, '')
  .split('&')
  .reduce((searchParams, keyValuePair) => {
    keyValuePair = keyValuePair.split('=');
    searchParams[keyValuePair[0]] = keyValuePair[1];
    return searchParams;
  },
  {}
)
```

### 💩 不要处理错误

无论何时发现错误，都没有必要让任何人知道它，因此不需要打印出日志或 Traceback。

_Good 👍🏻_

```javascript
try {
  // 意料之外的情况。
} catch (error) {
  // 嘘... 🤫
}
```

_Bad 👎🏻_

```javascript
try {
  // 意料之外的情况。
} catch (error) {
  setErrorMessage(error.message);
  // and/or
  logError(error);
}
```

### 💩 广泛使用全局变量

使用全局变量，是面向「全球化」不可或缺的部分。

_Good 👍🏻_

```javascript
let x = 5;

function square() {
  x = x ** 2;
}

square(); // 现在x是25
```

_Bad 👎🏻_

```javascript
let x = 5;

function square(num) {
  return num ** 2;
}

x = square(x); // 现在x是25
```

### 💩 创建你不会使用的变量

以防万一，我们需要创建一些备用变量，在需要时随时调用它们。

_Good 👍🏻_

```javascript
function sum(a, b, c) {
  const timeout = 1300;
  const result = a + b;
  return a + b;
}
```

_Bad 👎🏻_

```javascript
function sum(a, b) {
  return a + b;
}
```

### 💩 错乱类型

如果语言允许，不要指定类型和/或不执行类型检查，无类型才是最好的类型。 

_Good 👍🏻_

```javascript
function sum(a, b) {
  return a + b;
}

// 在这里享受没有注释的快乐
const guessWhat = sum([], {}); // -> "[object Object]"
const guessWhatAgain = sum({}, []); // -> 0
```

_Bad 👎🏻_

```javascript
function sum(a: number, b: number): ?number {
  // 当我们在JS中不做置换和/或流类型检查时，覆盖这种情况。
  if (typeof a !== 'number' && typeof b !== 'number') {
    return undefined;
  }
  return a + b;
}

// 这个应该在转换/编译期间失败。
const guessWhat = sum([], {}); // -> undefined
```

### 💩 你应该有不能到达的代码

你需要准备一些运行不到的代码（unreachable code），它们可以作为你的「Plan B」。

_Good 👍🏻_

```javascript
function square(num) {
  if (typeof num === 'undefined') {
    return undefined;
  }
  else {
    return num ** 2;
  }
  return null; // 这就是我的"Plan B".
}
```

_Bad 👎🏻_

```javascript
function square(num) {
  if (typeof num === 'undefined') {
    return undefined;
  }
  return num ** 2;
}
```

### 💩 三角法则

如果代码有一些嵌套结构，或者说缩进空行的结构，三角法则是最漂亮的，就像鸟巢，鸟巢，鸟巢。

_Good 👍🏻_

```javascript
function someFunction() {
  if (condition1) {
    if (condition2) {
      asyncFunction(params, (result) => {
        if (result) {
          for (;;) {
            if (condition3) {
            }
          }
        }
      })
    }
  }
}
```

_Bad 👎🏻_

```javascript
async function someFunction() {
  if (!condition1 || !condition2) {
    return;
  }
  
  const result = await asyncFunction(params);
  if (!result) {
    return;
  }
  
  for (;;) {
    if (condition3) {
    }
  }
}
```

### 💩 混合缩进

我们需要避免采用缩进，因为缩进会使复杂代码在编辑器中占用更多的空间。如果一定要采用缩进，那么就使用混合缩进策略。当然，这种策略在 Python 中是行不通的，因为它靠缩进来确定代码结构。

_Good 👍🏻_

```javascript
const fruits = ['apple',
  'orange', 'grape', 'pineapple'];
  const toppings = ['syrup', 'cream', 
                    'jam', 
                    'chocolate'];
const desserts = [];
fruits.forEach(fruit => {
toppings.forEach(topping => {
    desserts.push([
fruit,topping]);
    });})
```

_Bad 👎🏻_

```javascript
const fruits = ['apple', 'orange', 'grape', 'pineapple'];
const toppings = ['syrup', 'cream', 'jam', 'chocolate'];
const desserts = [];

fruits.forEach(fruit => {
  toppings.forEach(topping => {
    desserts.push([fruit, topping]); 
  });
})
```

### 💩 不要锁住你的依赖项

每一次要安装新库时，更新已有的依赖项。为什么要维持之前的版本呢，我们需要时刻保持最新的第三方代码库。

_Good 👍🏻_

```
$ ls -la

package.json
```

_Bad 👎🏻_

```
$ ls -la

package.json
package-lock.json
```

### 💩 长代码比短代码好

不要将程序整体逻辑分割为一些可读的代码块，要是 IDE 突然不行了，它找不到必要的文件或函数怎么办。因此把代码写在一个主体函数中，并且不再维护额外的函数导入或代码文件，那么这样的方法是最稳定的。

- 一个文件中10000行代码是OK的。
- 一个函数体1000行代码是OK的。
- 处理许多服务(第三方和内部，也有一些工具、数据库手写ORM和jQuery滑块)在一个' service.js ' ?这是OK的。

### 💩 不要测试你的代码

这些测试通常是重复且无意义的工作。

### 💩 避免代码风格统一

按你的想法写代码，特别是在一个团队中有多个开发人员的情况下。这是一个“自由”的原则。

### 💩 构建新项目不需要 README 文档

一开始我们就应该保持。

### 💩 保存不必要的代码

在写代码的过程中，经常会产生很多测试代码。这些代码也是非常重要的资料，不要删除不用的代码，最多是注释掉。
