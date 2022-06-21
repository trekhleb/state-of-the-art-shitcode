# 垃圾程式碼書寫準則

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

你專案中的程式碼只有在嚴格遵循如下列出的《垃圾程式碼書寫準則》的情況下，才可被稱之為編寫得當的垃圾程式碼。

_Read this in other languages:_
[_English_](README.md),
[_한국어_](README.ko-KR.md),
[_简体中文_](README.zh-CN.md)

## 獲取徽章

如果你的儲存庫遵循垃圾程式碼書寫準則，你應該用下面的 "state-of-the-art shitcode" 徽章：

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

引用徽章的 Markdown 語法：

```
[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)
```

## 準則

### 💩 用程式碼混淆器的方式命名變數

我們花越少時間打字，你就有越多的時間思考！

_Good 👍🏻_

```javascript
let a = 42;
```

_Bad 👎🏻_

```javascript
let age = 42;
```

### 💩 變數/函式混合命名風格

為不同慶祝一下。

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

### 💩 不要寫註釋

反正沒人會讀你的程式碼。

_Good 👍🏻_

```javascript
const cdr = 700;
```

_Bad 👎🏻_

更多時候，評論應該包含一些「為什麼」，而不是一些「是什麼」。如果「什麼」在程式碼中不清楚，那麼程式碼可能太混亂了。

```javascript
// 這裡的 700ms 是基於 UX 的 A/B Testing 測試結果的經驗所計算出來的。
// @see: <link to experiment or to related JIRA task or to something that explains number 700 in details>
const callbackDebounceRate = 700;
```

### 💩 使用母語寫註釋

如果您違反了「無註釋」原則，那麼至少嘗試用一種不同於您用來編寫程式碼的語言來編寫註釋。如果你的母語是英語，你可能會違反這個原則。

_Good 👍🏻_

```javascript
// 隱藏錯誤的彈跳視窗
toggleModal(false);
```

_Bad 👎🏻_

```javascript
// Hide modal window on error.
toggleModal(false);
```

### 💩 儘可能混合不同的格式

為不同慶祝一下。

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

### 💩 儘可能把程式碼寫成一行

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

### 💩 不要處理錯誤

無論何時發現錯誤，都沒有必要讓任何人知道它。不要有日誌，不要有錯誤彈跳視窗。

_Good 👍🏻_

```javascript
try {
  // 意料之外的情況。
} catch (error) {
  // tss... 🤫
}
```

_Bad 👎🏻_

```javascript
try {
  // 意料之外的情況。
} catch (error) {
  setErrorMessage(error.message);
  // and/or
  logError(error);
}
```

### 💩 廣泛地使用全域變數 (Global variables)

這是一個全球通用的準則。

_Good 👍🏻_

```javascript
let x = 5;

function square() {
  x = x ** 2;
}

square(); // 現在 x 是 25
```

_Bad 👎🏻_

```javascript
let x = 5;

function square(num) {
  return num ** 2;
}

x = square(x); // 現在 x 是 25
```

### 💩 建立你不會使用的變數

以防萬一。

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

### 💩 如果程式語言允許，千萬不要指定型別或執行型別檢查

_Good 👍🏻_

```javascript
function sum(a, b) {
  return a + b;
}

// 在這裡享受沒有型別標示的快樂
const guessWhat = sum([], {}); // -> "[object Object]"
const guessWhatAgain = sum({}, []); // -> 0
```

_Bad 👎🏻_

```javascript
function sum(a: number, b: number): ?number {
  // 當我們在 JS 中不做轉譯或 Flow 型別檢查時，要額外進行以下檢查
  if (typeof a !== 'number' && typeof b !== 'number') {
    return undefined;
  }
  return a + b;
}

// 這個應該在轉譯或編譯的時候發生失敗
const guessWhat = sum([], {}); // -> undefined
```

### 💩 你應該擁有一段不能到達的程式碼

永遠要有一套自己的第二計畫 ("Plan B")。

_Good 👍🏻_

```javascript
function square(num) {
  if (typeof num === 'undefined') {
    return undefined;
  }
  else {
    return num ** 2;
  }
  return null; // 這就是我的 "Plan B"
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

### 💩 三角法則

想隻鳥一樣 —— 築巢、築巢、築巢。

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

### 💩 混合縮排

避免縮排，因為它們會使複雜的程式碼在編輯器中佔用更多的空間。如果你不喜歡迴避他們，那就和他們一起亂吧。

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

### 💩 不要鎖定你的相依套件 (Node.js)

以不受控的方式更新每個新安裝的相依套件。為什麼堅持使用過去的版本？讓我們使用最新、最潮的函式庫版本吧！

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

### 💩 永遠將所有的布林值取名為 `flag` 就好

留一些空間給你的同事去思考這個布林值所代表的意義。

_Good 👍🏻_

```javascript
let flag = true;
```

_Bad 👎🏻_

```javascript
let isDone = false;
let isEmpty = false;
```

### 💩 函式的程式碼行數寫的短不如寫的長

不要把程式碼邏輯切分成多個易讀的部分。想想如果 IDE 的搜尋功能停止運作，您將無法找到所需的檔案或函式！

- 一個檔案中 10000 行程式碼是 OK 的。
- 一個函式的程式碼行數有 1000 行是 OK 的。
- 在一個 `service.js` 中處理許多服務(第三方函式庫和內部函式庫、一些工具、手刻 ORM 與 jQuery slider)？這是 OK 的！

### 💩 不要測試你的程式碼

這是個重複且多餘的工作。

### 💩 盡可能的避免程式碼風格統一

程式碼想怎麼寫就怎麼寫，尤其是在一個團隊中有多位開發人員的情況下。這就是「自由」的基本原則。

### 💩 新專案不需要 README 文件

我們應該從一開始就保持著這種習慣。

### 💩 你需要保留一些用不到的程式碼

不要刪除用不到的程式碼，最多就是加上註解即可。
