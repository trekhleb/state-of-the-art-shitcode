# State-of-the-Art Shitcode Principles

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

هذه قائمة بأحدث مبادئ كود shitcode التي يجب أن يتبعها مشروعك ليطلق عليه كود shitcode المناسب.

_اقرأ هذا في لغات أخرى:_
[_English_](README.md),
[_简体中文_](README.zh-CN.md),
[_한국어_](README.ko-KR.md)

## احصل على شارتك

إذا كان repository الخاص بك يتبع أحدث مبادئ كود shitcode, فيمكنك استخدام شارة 'state-of-the-art shitcode' التالي:

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

مصدر-الكود للشارة:

```
[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)
```

## المبادئ

### 💩 تسمية المتغيرات بطريقة كما لو كانت شفرتك غامضة بالفعل

ضغطات أقل على المفاتيح, ووقت أكثر لك.

_جيد 👍🏻_

```javascript
let a = 42;
```

_سيئ 👎🏻_

```javascript
let age = 42;
```

### 💩 امزج أسلوب تسمية المتغير / الوظائف

احتفل بالفرق.

_جيد 👍🏻_

```javascript
let wWidth = 640;
let w_height = 480;
```

_سيئ 👎🏻_

```javascript
let windowWidth = 640;
let windowHeight = 480;
```

### 💩 أبدًا لا تكتب تعليقات

لن يقرأ أحد الكود الخاص بك على أي حال.

_جيد 👍🏻_

```javascript
const cdr = 700;
```

_سيئ 👎🏻_

في كثير من الأحيان يجب أن تحتوي التعليقات على بعض 'لماذا' وليس 'ماذا'. إذا لم يكن 'ماذا' واضحًا في الكود, فمن المحتمل أن يكون الكود فوضويًا للغاية.

```javascript
// The number of 700ms has been calculated empirically based on UX A/B test results.
// @see: <link to experiment or to related JIRA task or to something that explains number 700 in details>
const callbackDebounceRate = 700;
```

### 💩 اكتب دائمًا التعليقات بلغتك الأم

إذا انتهكت مبدأ 'لا تعليقات', فحاول على الأقل كتابة تعليقات بلغة مختلفة عن اللغة التي تستخدمها لكتابة الشفرة. إذا كانت لغتك الأم هي الإنجليزية, فقد تنتهك هذا المبدأ.

_جيد 👍🏻_

```javascript
// Закриваємо модальне віконечко при виникненні помилки.
toggleModal(false);
```

_سيئ 👎🏻_

```javascript
// Hide modal window on error.
toggleModal(false);
```

### 💩 حاول مزج نمط التنسيق قدر الإمكان

احتفل بالفرق.

_جيد 👍🏻_

```javascript
let i = ["tomato", "onion", "mushrooms"];
let d = ["ketchup", "mayonnaise"];
```

_سيئ 👎🏻_

```javascript
let ingredients = ["tomato", "onion", "mushrooms"];
let dressings = ["ketchup", "mayonnaise"];
```

### 💩 ضع أكبر قدر ممكن من الكود في سطر واحد

_جيد 👍🏻_

```javascript
document.location.search
  .replace(/(^\?)/, "")
  .split("&")
  .reduce(function (o, n) {
    n = n.split("=");
    o[n[0]] = n[1];
    return o;
  }, {});
```

_سيئ 👎🏻_

```javascript
document.location.search
  .replace(/(^\?)/, "")
  .split("&")
  .reduce((searchParams, keyValuePair) => {
    keyValuePair = keyValuePair.split("=");
    searchParams[keyValuePair[0]] = keyValuePair[1];
    return searchParams;
  }, {});
```

### 💩 افشل بصمت

عند اكتشاف خطأ ما, ليس من الضروري أن يعرفه أحد. لا سجلات, لا أنماط الخطأ, استرخي.

_جيد 👍🏻_

```javascript
try {
  // Something unpredictable.
} catch (error) {
  // tss... 🤫
}
```

_سيئ 👎🏻_

```javascript
try {
  // Something unpredictable.
} catch (error) {
  setErrorMessage(error.message);
  // and/or
  logError(error);
}
```

### 💩 استخدام متغيرات global على نطاق واسع

مبدأ العولمة.

_جيد 👍🏻_

```javascript
let x = 5;

function square() {
  x = x ** 2;
}

square(); // Now x is 25.
```

_سيئ 👎🏻_

```javascript
let x = 5;

function square(num) {
  return num ** 2;
}

x = square(x); // Now x is 25.
```

### 💩 قم بإنشاء متغيرات لن تستخدمها.

تحسبُاً.

_جيد 👍🏻_

```javascript
function sum(a, b, c) {
  const timeout = 1300;
  const result = a + b;
  return a + b;
}
```

_سيئ 👎🏻_

```javascript
function sum(a, b) {
  return a + b;
}
```

### 💩 لا تحدد الأنواع و/أو لا تفعل عمليات التحقق من الكتابة إذا كانت اللغة تسمح لك بذلك.

_جيد 👍🏻_

```javascript
function sum(a, b) {
  return a + b;
}

// Having untyped fun here.
const guessWhat = sum([], {}); // -> "[object Object]"
const guessWhatAgain = sum({}, []); // -> 0
```

_سيئ 👎🏻_

```javascript
function sum(a: number, b: number): ?number {
  // Covering the case when we don't do transpilation and/or Flow type checks in JS.
  if (typeof a !== "number" && typeof b !== "number") {
    return undefined;
  }
  return a + b;
}

// This one should fail during the transpilation/compilation.
const guessWhat = sum([], {}); // -> undefined
```

### 💩 يجب أن يكون لديك جزء من الكود لا يمكن الوصول إليه

هذه هي "خطتك ب".

_جيد 👍🏻_

```javascript
function square(num) {
  if (typeof num === "undefined") {
    return undefined;
  } else {
    return num ** 2;
  }
  return null; // This is my "Plan B".
}
```

_سيئ 👎🏻_

```javascript
function square(num) {
  if (typeof num === "undefined") {
    return undefined;
  }
  return num ** 2;
}
```

### 💩 مبدأ المثلث

كن مثل الطائر - nest, nest, nest.

_جيد 👍🏻_

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
      });
    }
  }
}
```

_سيئ 👎🏻_

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

### 💩 العبث مع المسافات البادئة

تجنب المسافات البادئة لأنها تجعل الكود معقد, يشغل مساحة أكبر في المحرر. إذا كنت لا ترغب في تجنبهم, فما عليك سوى العبث معهم.

_جيد 👍🏻_

```javascript
const fruits = ["apple", "orange", "grape", "pineapple"];
const toppings = ["syrup", "cream", "jam", "chocolate"];
const desserts = [];
fruits.forEach((fruit) => {
  toppings.forEach((topping) => {
    desserts.push([fruit, topping]);
  });
});
```

_سيئ 👎🏻_

```javascript
const fruits = ["apple", "orange", "grape", "pineapple"];
const toppings = ["syrup", "cream", "jam", "chocolate"];
const desserts = [];

fruits.forEach((fruit) => {
  toppings.forEach((topping) => {
    desserts.push([fruit, topping]);
  });
});
```

### 💩 لا تقفل dependencies الخاصة بك

قم بتحديث تبعياتك على كل تثبيت جديد بطريقة غير خاضعة للرقابة. لماذا نتمسك بالماضي, دعنا نستخدم أحدث إصدارات المكتبات.

_جيد 👍🏻_

```
$ ls -la

package.json
```

_سيئ 👎🏻_

```
$ ls -la

package.json
package-lock.json
```

### 💩 قم دائمًا بتسمية القيمة المنطقية بـ `flag`

اترك مساحة لزملائك للتفكير في معنى القيمة المنطقية.

_جيد 👍🏻_

```javascript
let flag = true;
```

_سيئ 👎🏻_

```javascript
let isDone = false;
let isEmpty = false;
```

### 💩 قرائة الوظائف الطويلة افضل من القصيرة

لا تقسم منطق البرنامج إلى أجزاء يمكن قراءتها. ماذا لو تعطل بحث IDE الخاص بك ولم تتمكن من العثور على الملف أو الوظيفة اللازمة؟

- 10000 سطر من الكود في ملف واحد جيد.
- 1000 سطر من الكود في ملف واحد جيد.
- التعامل مع العديد من الخدمات (طرف ثالث وداخلي, أيضا, هناك بعض المساعدين, database hand-written ORM jQuery slider) في `service.js` واحد؟ جيد.

### 💩 تجنب تغطية الكود الخاص بك بالاختبارات

هذا هو كمية مكررة وغير ضرورية من العمل.

### 💩 بأقصى ما يمكنك تجنب code linters

اكتب الكود كما تريد, خاصة إذا كان هناك أكثر من مطور واحد في الفريق. هذا هو مبدأ "الحرية".

### 💩 ابدأ مشروعك بدون ملف README.

واحتفظ بها بهذه الطريقة في الوقت الحالي.

### 💩 يجب أن يكون لديك كود غير ضروري

لا تحذف الكود الذي لا يستخدمه تطبيقك. على الأكثر, قم بالتعليق عليه.
