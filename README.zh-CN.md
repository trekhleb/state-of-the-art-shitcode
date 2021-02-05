# 垃圾代码书写准则

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

这是一个你的项目应该遵循的垃圾代码书写准则的列表，把称为适当的垃圾代码。

_Read this in other languages:_
[_English_](README.md),
[_한국어_](README.ko-KR.md)

## 获取徽章

如果你的仓库遵循垃圾代码书写准则，你应该用下面的"state-of-the-art shitcode" 徽章：

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

标记徽章的源代码:

```
[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)
```

## 准则

### 💩 以一种代码已经被混淆的方式命名变量

如果我们键入的东西越少，那么就有越多的时间去思考代码逻辑等问题。

_Good 👍🏻_

```javascript
let a = 42;
```

_Bad 👎🏻_

```javascript
let age = 42;
```

### 💩 变量/函数混合命名风格

为不同庆祝一下。

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

反正没人会读你的代码。

_Good 👍🏻_

```javascript
const cdr = 700;
```

_Bad 👎🏻_

更多时候，注释应该包含一些“为什么”，而不是一些“是什么”。如果代码本身不能讲清楚“是什么”，那么这段代码可能太混乱了。

```javascript
// The number of 700ms has been calculated empirically based on UX A/B test results.
// @see: <详细解释700的一个链接>
const callbackDebounceRate = 700;
```

### 💩 使用母语写注释

如果你违反了“无注释”原则，那么至少尝试用一种不同于你用来编写代码的语言来编写注释。如果你的母语是英语，你可以违反这个原则。

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

为不同庆祝一下。

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

无论何时发现错误，都没有必要让任何人知道它。不要日志，不要错误弹框，问题不大。

_Good 👍🏻_

```javascript
try {
  // 意料之外的情况。
} catch (error) {
  // tss... 🤫
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

### 💩 尽量使用全局变量

全球化的原则。

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

以防万一。

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

### 💩 如果语言允许，不要指定类型和/或不执行类型检查。

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

这是你的 "Plan B".

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

就像乌龟一样。缩进。缩进。缩进。

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

避免缩进，它们会使复杂的代码在编辑器中占用更多的空间。如果你不喜欢回避缩进，那就胡乱缩进。

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

以非受控方式更新每个新安装的依赖项。何必固步自封，让我们使用最先进的库版本。

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

### 💩 函数长的比短的好

不要把程序逻辑分成可读的部分。如果IDE的搜索停止，而你无法找到所需的文件或函数，该怎么办?

- 一个文件中10000行代码是OK的。
- 一个函数体有1000行代码是OK的。
- 在一个' service.js ' 中处理许多服务(第三方库和内部库、一些工具、手写的数据库ORM和jQuery滑块)? 这是OK的。

### 💩 不要测试你的代码

这是重复且非必要的工作。

### 💩 避免代码风格统一

想怎么写代码就怎么写代码，特别是在一个团队中有多个开发人员的情况下。这是“自由”原则。

### 💩 构建新项目不需要 README 文档

一开始我们就应该保持。

### 💩 保存不必要的代码

不要删除不用的代码，最多注释掉。
