# 垃圾代码书写准则

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

你项目中的代码只有在严格遵循如下列出的《先进垃圾代码书写准则》的情况下，才可被称之为编写得当的垃圾代码。

_Read this in other languages:_
[_English_](README.md),
[_한국어_](README.ko-KR.md)

## 获取徽章

如果你的仓库遵循垃圾代码书写准则，你应该用下面的"state-of-the-art shitcode" 徽章：

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

引入徽章的Markdown代码:

```
[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)
```

## 准则

### 💩 用代码混淆器的方式命名变量

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

更多时候，评论应该包含一些“为什么”，而不是一些“是什么”。如果“什么”在代码中不清楚，那么代码可能太混乱了。

```javascript
// 700ms的数值是根据UX A/B测试结果算出的经验数值。
// @查看: <详细解释700的一个链接>
const callbackDebounceRate = 700;
```

### 💩 使用母语写注释

如果您违反了“无注释”原则，那么至少尝试用一种不同于您用来编写代码的语言来编写注释。如果你的母语是英语，你可能会违反这个原则。

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

无论何时发现错误，都没有必要让任何人知道它。不要有日志，不要有错误弹框。

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

### 💩 广泛使用全局（global）变量

全球化（globalization）的原则。

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

// 在此调用无类型的函数
const guessWhat = sum([], {}); // -> "[object Object]"
const guessWhatAgain = sum({}, []); // -> 0
```

_Bad 👎🏻_

```javascript
function sum(a: number, b: number): ?number {
  // 处理在JS中不做转译或不做Flow类型检查，或两者都不做的情况。
  if (typeof a !== 'number' && typeof b !== 'number') {
    return undefined;
  }
  return a + b;
}

// 这个应该在转译或编译期间报错。
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

像套娃一样：嵌套、嵌套、嵌套！

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

避免缩进，因为它们会使复杂的代码在编辑器中占用更多的空间。如果觉得避免缩进太麻烦，那就随便排版。

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

在软件的每一次安装过程中以非受控方式更新依赖项。为什么坚持使用老版本？让我们使用最新版本的库。

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

不要把程序逻辑分成可读的部分。如果IDE的搜索功能出问题了，而您无法找到所需的文件或函数，该怎么办?

- 一个文件中有10000行代码是OK的。
- 一个函数体有1000行代码是OK的。
- 在一个' service.js ' 中处理许多服务(第三方库和内部库、一些工具、手写的数据库ORM和jQuery滑块)? 这是OK的。

### 💩 不要测试你的代码

这是重复且无用的工作。

### 💩 避免代码风格统一

随意编写你的代码，特别是在一个团队中有多个开发人员的情况下。这是“自由”原则。

### 💩 构建新项目不需要 README 文档

自始至终确保项目中无README。

### 💩 保存不必要的代码

不要删除不用的代码，最多注释掉。
