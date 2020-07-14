# 垃圾代码书写准则

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

这里是垃圾代码书写准则，你的代码只有遵循这里的条例，才能算上是真正的“烂代码”。

_Read this in other languages:_
[_English_](https://github.com/trekhleb/state-of-the-art-shitcode)

## 获取徽章

如果你的代码仓库遵循了垃圾代码书写准则，你可以考虑使用下面的“烂代码”徽章：

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

Markdown 链接为：

```
[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)
```

## 准则

### 💩 用混淆代码的方式来混淆变量的名字

打字越少，节约的时间越多哦。

_Good 👍🏻_

```javascript
let a = 42;
```

_Bad 👎🏻_

```javascript
let age = 42;
```

### 💩 用多种混合的风格来命名变量或者函数

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

应该多写一些解释原因的注释，而不是描述性的注释。因为如果从代码里面都看不出来这到底是啥的话，大概可能也许就是因为代码太乱了。

```javascript
// 700ms 是根据 UX A/B 测试的结果进行计算得出的。
// @see: <一个指向详细解释这个 700 是啥的链接>
const callbackDebounceRate = 700;
```

### 💩 用母语写注释

如果您违反了“无注释”原则，那么还是建议您用与代码内容不同的语言来写注释。而如果您的母语是英语，可能就会违反这个原则。

_Good 👍🏻_

```javascript
// 当发生错误的时候，隐藏弹窗
toggleModal(false);
```

_Bad 👎🏻_

```javascript
// Hide modal window on error.
toggleModal(false);
```

### 💩 尽可能地去混合代码格式

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

### 💩 尽可能地把代码写成一行

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

### 💩 别在意错误

无论您什么时候发现了问题，都没必要让别人知道。这样又没有日志，又没有弹窗，岂不美哉？

_Good 👍🏻_

```javascript
try {
  // 也许会发生错误的代码
} catch (error) {
  // 嘘... 🤫
}
```

_Bad 👎🏻_

```javascript
try {
  // 也许会发生错误的代码
} catch (error) {
  setErrorMessage(error.message);
  // and/or
  logError(error);
}
```

### 💩 广泛使用全局变量

所谓全局原则。

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

### 💩 创建一些你用不到的变量

以防万一呢。

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

### 💩 如果可以，不要规定类型也不要做类型检查

_Good 👍🏻_

```javascript
function sum(a, b) {
  return a + b;
}

// 享受不被类型系统约束的快乐吧
const guessWhat = sum([], {}); // -> "[object Object]"
const guessWhatAgain = sum({}, []); // -> 0
```

_Bad 👎🏻_

```javascript
function sum(a: number, b: number): ?number {
  // 如果不做类型检查或者转译的话，就这样子
  if (typeof a !== 'number' && typeof b !== 'number') {
    return undefined;
  }
  return a + b;
}

// 这行代码会在编译时出错
const guessWhat = sum([], {}); // -> undefined
```

### 💩 你需要写一些不会被执行的代码

这是你的 B 计划。

_Good 👍🏻_

```javascript
function square(num) {
  if (typeof num === 'undefined') {
    return undefined;
  }
  else {
    return num ** 2;
  }
  return null; // 这就是我的 B 计划！
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

就像鸟巢巢巢巢巢巢巢巢巢一样~

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

不要用缩进！因为在复杂的代码里面，缩进会占据更多的空间呢。如果你还是想要缩进的话就放飞自我吧。

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

### 💩 不要锁定依赖

用不受控的方式来更新依赖。为什么偏要坚持用旧版？让我们一起用最前沿的版本吧！

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

### 💩 把布尔值都命名为 `flag`

给你同事思考的空间，让他们想想这个布尔值到底指的啥。

_Good 👍🏻_

```javascript
let flag = true;
```

_Bad 👎🏻_

```javascript
let isDone = false;
let isEmpty = false;
```

### 💩 函数长的比短的好

不要为了可读性而把程序的逻辑拆开了。万一 IDE 的搜索功能坏掉了，找不到你想要的文件或者函数了，咋办呐？

- 把一万行代码放进一个文件里是个很棒的选择。
- 把一千行代码放进一个函数里也是一个不错的想法。
- 把库(比如第三方的库或者自己的轮子，还有一些工具、数据库、手写的 ORM 和 jQuery 脚手架)都放在一个'service.js'里也是 OK 的。

### 💩 不要往代码里加测试代码

这很多余而且没必要。

### 💩 极力抵制代码格式化

想写啥样写啥样，尤其在团队协作的时候——这叫做“自由”主义。

### 💩 不要在项目初始化的时候加入 README

并且之后也别加呢。

### 💩 把没用的代码留下来

别删啊，把它们注释掉就好了嘛。
