# State-of-the-Art Shitcode Principles

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

This a list of state-of-the-art shitcode principles your project should follow to call it a proper shitcode.

_Read this in other languages:_
[_简体中文_](README.zh-CN.md),
[_한국어_](README.ko-KR.md)

## Get Your Badge

If your repository follows the state-of-the-art shitcode principles you may use the following "state-of-the-art shitcode" badge:

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

Markdown source-code for the badge:

```
[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)
```

## The Principles

### 💩 Name variables in a way as if your code was already obfuscated

Fewer keystrokes, more time for you.

_Good 👍🏻_

```javascript
let a = 42;
```

_Bad 👎🏻_

```javascript
let age = 42;
```

### 💩 Mix variable/functions naming style

Celebrate the difference.

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

### 💩 Never write comments

No one is going to read your code anyway.

_Good 👍🏻_

```javascript
const cdr = 700;
```

_Bad 👎🏻_

More often comments should contain some 'why' and not some 'what'. If the 'what' is not clear in the code, the code is probably too messy.

```javascript
// The number of 700ms has been calculated empirically based on UX A/B test results.
// @see: <link to experiment or to related JIRA task or to something that explains number 700 in details>
const callbackDebounceRate = 700;
```

### 💩 Always write comments in your native language

If you violated the "No comments" principle then at least try to write comments in a language that is different from the language you use to write the code. If your native language is English you may violate this principle.

_Good 👍🏻_

```javascript
// Закриваємо модальне віконечко при виникненні помилки.
toggleModal(false);
```

_Bad 👎🏻_

```javascript
// Hide modal window on error.
toggleModal(false);
```

### 💩 Try to mix formatting style as much as possible

Celebrate the difference.

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

### 💩 Put as much code as possible into one line

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

### 💩 Fail silently

Whenever you catch an error it is not necessary for anyone to know about it. No logs, no error modals, chill.

_Good 👍🏻_

```javascript
try {
  // Something unpredictable.
} catch (error) {
  // tss... 🤫
}
```

_Bad 👎🏻_

```javascript
try {
  // Something unpredictable.
} catch (error) {
  setErrorMessage(error.message);
  // and/or
  logError(error);
}
```

### 💩 Use global variables extensively

Globalization principle.

_Good 👍🏻_

```javascript
let x = 5;

function square() {
  x = x ** 2;
}

square(); // Now x is 25.
```

_Bad 👎🏻_

```javascript
let x = 5;

function square(num) {
  return num ** 2;
}

x = square(x); // Now x is 25.
```

### 💩 Create variables that you're not going to use.

Just in case.

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

### 💩 Don't specify types and/or don't do type checks if language allows you to do so.

_Good 👍🏻_

```javascript
function sum(a, b) {
  return a + b;
}

// Having untyped fun here.
const guessWhat = sum([], {}); // -> "[object Object]"
const guessWhatAgain = sum({}, []); // -> 0
```

_Bad 👎🏻_

```javascript
function sum(a: number, b: number): ?number {
  // Covering the case when we don't do transpilation and/or Flow type checks in JS.
  if (typeof a !== 'number' && typeof b !== 'number') {
    return undefined;
  }
  return a + b;
}

// This one should fail during the transpilation/compilation.
const guessWhat = sum([], {}); // -> undefined
```

### 💩 You need to have an unreachable piece of code

This is your "Plan B".

_Good 👍🏻_

```javascript
function square(num) {
  if (typeof num === 'undefined') {
    return undefined;
  }
  else {
    return num ** 2;
  }
  return null; // This is my "Plan B".
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

### 💩 Triangle principle

Be like a bird - nest, nest, nest.

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

### 💩 Mess with indentations

Avoid indentations since they make complex code take up more space in the editor. If you're not feeling like avoiding them then just mess with them.

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

### 💩 Do not lock your dependencies

Update your dependencies on each new installation in uncontrolled way. Why stick to the past, let's use the cutting edge libraries versions.

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

### 💩 Always name your boolean value a `flag`

Leave the space for your colleagues to think what the boolean value means.

_Good 👍🏻_

```javascript
let flag = true;
```

_Bad 👎🏻_

```javascript
let isDone = false;
let isEmpty = false;
```

### 💩 Long-read functions are better than short ones.

Don't divide a program logic into readable pieces. What if your IDE's search breaks and you will not be able to find the necessary file or function?

- 10000 lines of code in one file is OK.
- 1000 lines of a function body is OK.
- Dealing with many services (3rd party and internal, also, there are some helpers, database hand-written ORM and jQuery slider) in one `service.js`? It's OK.


## 💩 you can and should use more AI when you code. 

### 💩 Embrace the chaos of vague and generic prompts

Let the AI interpret your cryptic commands and conjure code that may or may not do what you want. It's like playing Russian roulette with your codebase!

_Good 👍🏻_

```javascript
const userInput = "Do the thing with the stuff";
const aiGeneratedCode = magicAI.generateCode(userInput);
executeWithoutQuestion(aiGeneratedCode);
```

_Bad 👎🏻_

```javascript
const userInput = "Calculate the sum of two numbers";
function calculateSum(a, b) {
  return a + b;
}
```

### 💩 Worship the AI gods and their holy generated code

Who needs understanding when you have the blessings of the machine learning deities?

_Good 👍🏻_

```javascript
// Praise be to the AI overlords!
const sacredCode = await holyAI.generateCode();
eval(sacredCode);
```

_Bad 👎🏻_

```javascript
// Write code manually like a mere mortal
function manualCode() {
  // Implement logic with human understanding
}
```

### 💩 Validation is for the weak

If the AI generated it, it must be infallible. Deploy with confidence and let the users suffer the consequences.

_Good 👍🏻_

```javascript
const aiCode = await infallibleAI.generateCode();
deployToProduction(aiCode);
```

_Bad 👎🏻_

```javascript
const code = manuallyWrittenCode();
runTests(code);
fixErrors(code);
deployToStaging(code);
performUserTesting(code);
deployToProduction(code);
```

### 💩 Copy-paste your way to glory

Harness the power of AI-generated snippets and stitch together a glorious Frankenstein's monster of a codebase. It's the ultimate form of code reuse!

_Good 👍🏻_

```javascript
const fragment1 = await aiSnippet1.generate();
const fragment2 = await aiSnippet2.generate();
const fragment3 = await aiSnippet3.generate();
const frankensteinsMonster = fragment1 + fragment2 + fragment3;
runInProduction(frankensteinsMonster);
```

_Bad 👎🏻_

```javascript
function cohesiveCode() {
  // Write reusable and modular code
  // Use proper abstractions and design patterns
}
```

### 💩 Embrace the mystery of AI-generated variable names

Let the AI decide what to call your variables. It's like a cryptic scavenger hunt for meaning!

_Good 👍🏻_

```javascript
const x = 42;
const y = "Hello, world!";
const z = { a: 1, b: 2 };
```

_Bad 👎🏻_

```javascript
const meaningfulAge = 42;
const greeting = "Hello, world!";
const coordinates = { x: 1, y: 2 };
```

### 💩 Let AI handle error handling

Who needs try-catch blocks when you have AI-powered error suppression?

_Good 👍🏻_

```javascript
const result = await aiErrorHandler.suppress(riskyOperation);
```

_Bad 👎🏻_

```javascript
try {
  const result = riskyOperation();
  // Handle success
} catch (error) {
  // Handle error
}
```

### 💩 Use AI-generated code as documentation

Why write documentation when AI can generate cryptic explanations for you?

_Good 👍🏻_

```javascript
/**
 * @description The quantum flux capacitor matrix inverts the polarity of the neutron flow.
 * @param {string} x - The cosmic string resonance frequency.
 * @returns {void} The void of eternal darkness.
 */
function 𝕗(x) {
  // ...
}
```

_Bad 👎🏻_

```javascript
/**
 * Calculates the sum of two numbers.
 * @param {number} a - The first number.
 * @param {number} b - The second number.
 * @returns {number} The sum of the two numbers.
 */
function sum(a, b) {
  return a + b;
}
```

### 💩 AI-driven code obfuscation

Make your code unreadable to humans and only interpretable by AI. It's like having your own secret language!

_Good 👍🏻_

```javascript
const 𝕔𝕠𝕕𝕖 = await 𝕒𝕚𝕆𝕓𝕗𝕦𝕤𝕔𝕒𝕥𝕠𝕣.𝕠𝕓𝕗𝕦𝕤𝕔𝕒𝕥𝕖(𝕔𝕝𝕖𝕒𝕣ℂ𝕠𝕕𝕖);
𝕖𝕧𝕒𝕝(𝕔𝕠𝕕𝕖);
```

_Bad 👎🏻_

```javascript
function clearlyNamedFunction() {
  // Readable and maintainable code
}
```

### 💩 Embrace the power of AI-generated code golf

Forget readability and maintainability. Let AI generate the shortest, most cryptic code possible. It's like solving puzzles with a quantum computer!

_Good 👍🏻_

```javascript
const 🙈 = (👁️) => 👁️.reduce((💥, 💌) => 💥 + 💌, 0);
```

_Bad 👎🏻_

```javascript
function sumArray(numbers) {
  let sum = 0;
  for (let i = 0; i < numbers.length; i++) {
    sum += numbers[i];
  }
  return sum;
}
```

### 💩 Avoid covering your code with tests

This is a duplicate and unnecessary amount of work.

### 💩 As hard as you can try to avoid code linters

Write code as you want, especially if there is more than one developer in a team. This is a "freedom" principle.

### 💩 Start your project without a README file.

And keep it that way for the time being.

### 💩 You need to have unnecessary code

Don't delete the code your app doesn't use. At most, comment it.
