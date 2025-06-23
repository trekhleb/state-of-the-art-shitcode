# 垃圾代码书写准则

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

你项目中的代码只有在严格遵循如下列出的《先进垃圾代码书写准则》的情况下，才可被称为编写得当的垃圾代码。

_Read this in other languages:_
[_English_](README.md),
[_한국어_](README.ko-KR.md)

## 获取徽章

如果你的仓库遵循垃圾代码书写准则，你应该引入下面的"state-of-the-art shitcode" 徽章：

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

引入徽章的Markdown代码:

```
[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)
```

## 准则

### 💩 用代码混淆器的方式命名变量

花越少的时间打字，就有越多的时间思考代码逻辑等问题。

_Good 👍🏻_

```javascript
let a = 42;
```

_Bad 👎🏻_

```javascript
let age = 42;
```

### 💩 变量/函数混合命名风格

为多样性喝彩。

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

### 💩 绝不写注释

反正没人会读你的代码。

_Good 👍🏻_

```javascript
const cdr = 700;
```

_Bad 👎🏻_

注释内容往往应该解释“为什么做某事”，而非代码“做了什么事”。  
如果代码本身无法清晰体现它“做了什么事”，那么代码可能太混乱了。

```javascript
// 700ms的数值是根据UX A/B测试结果算出的经验数值。
// @查看: <指向相关的JIRA task或者实验记录的链接（链接内容详细解释如何得出700这一数值）>
const callbackDebounceRate = 700;
```

### 💩 使用母语写注释

如果您违反了“无注释”原则，那么起码要用母语来编写注释，而您的母语最好与编程语言对应的自然语言不同。  
注意：如果你的母语是英语，你多半会违反这个原则。

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

### 💩 尽可能混合使用不同的格式

为多样性喝彩。

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

### 💩 出现异常时保持安静

无论何时捕获异常，都没有必要让任何人知道它。保持镇静——不要记录日志，不要显示错误弹窗。

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

因为考虑问题要有全局意识。

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

### 💩 提前创建此刻用不上的变量

万一用上了呢。

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

### 💩 如果语言允许，不要声明类型，不要执行类型检查

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

### 💩 应该保留不可达的代码

万一用上了呢？有备无患。

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

尽量避免缩进，代码变得复杂时缩进会占用很多屏幕空间。如果觉得避免缩进太麻烦，那就随便排版。

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

### 💩 不要锁定依赖项

在软件的每一次安装过程中以非受控方式更新依赖项。为什么抱着老版本不放？让我们使用最新版本的依赖。

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

### 💩 布尔变量命名应统一为 `flag`

给同事们留下点想象空间，让他们去猜测布尔值的真实含义。

_Good 👍🏻_

```javascript
let flag = true;
```

_Bad 👎🏻_

```javascript
let isDone = false;
let isEmpty = false;
```

### 💩 函数体写得越长越好

不要把程序逻辑拆分成易于阅读的小块，并且分别保存到不同的文件中。万一 IDE 的搜索功能出 bug 了，你没法通过搜索功能寻找文件或函数了怎么办？ 

- 一个文件写一万行代码是可以的。  
- 一个函数体写一千行也是没问题的。  
- 在同一个 `service.js` 文件里处理多种服务（三方库和内部库、工具类、手写的数据库 ORM 和一个 jQuery 滑块组件），这同样很好。
     

### 💩 不要测试你的代码

这是重复且无用的工作。

### 💩 避免代码风格统一

随意编写你的代码，特别是在一个团队中有多个开发人员的情况下。这是“自由”原则。

### 💩 启动新项目时不要写 README 文档

并且自始至终确保项目中无README。

### 💩 保存不必要的代码

不要删除不用的代码，最多注释掉。
