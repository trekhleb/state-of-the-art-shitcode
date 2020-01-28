# State-of-the-Art Shitcode Principles

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

## Get Your Badge

If your repository follows the state-of-the-art shitcode principles you may use the "state-of-the-art shitcode" badge:

```
[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)
```

## The Principles

### 💩 Name variables in a way as if your code was already obfuscated

Less keystrokes, more time for you.

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

Good 👍🏻

```javascript
let wWidth = 640;
let w_height = 480;
```

Bad 👎🏻

```javascript
let windowWidth = 640;
let windowHeight = 480;
```

### 💩 Never write comments

No one is going to write your code anyway.

Good 👍🏻

```javascript
const cdr = 700;
```

Bad 👎🏻

```javascript
// Callback function debounce rate in milliseconds.
const callbackDebounceRate = 700;
```

### 💩 Always write comments in your native language

_If your native language is English you may violate this rule_

Good 👍🏻

```javascript
// Закриваємо модальне віконечко при виникненні помилки.
toggleModal(false);
```

Bad 👎🏻

```javascript
// Hide modal window on error.
toggleModal(false);
```