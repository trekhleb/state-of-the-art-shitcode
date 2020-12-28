# State-of-the-Art Shitcode의 규칙

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

이 목록은 여러분의 프로젝트가 제대로 shitcode가 되기 위해 따라야 하는 규칙들입니다.

_다른 언어로 읽기:_
[_English_](README.md),
[_简体中文_](README.zh-CN.md)

## 뱃지 만들기

만일 여러분의 레포지토리가 shitcode의 규칙을 따른다면, 여러분은 다음과 같은 "state-of-the-art shitcode" 뱃지를 사용할 수 있습니다:

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

뱃지를 만들기 위한 마크다운 소스코드:

```
[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)
```

## 규칙

### 💩 변수 이름 애매하게 지정하기

적은 키 입력은, 여러분의 시간을 아끼게 해줍니다.

_Good 👍🏻_

```javascript
let a = 42;
```

_Bad 👎🏻_

```javascript
let age = 42;
```

### 💩 변수와 함수의 이름 스타일을 섞기

다양성을 축하합시다.

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

### 💩 주석을 전혀 작성하지 않기

어차피 아무도 당신의 코드를 읽지 않을 것입니다.

_Good 👍🏻_

```javascript
const cdr = 700;
```

_Bad 👎🏻_

자주 작성되는 주석은 '왜'가 아니라 '무엇'인지를 포함해야 합니다. 만일 코드에서 '무엇'이 명확하지 않으면, 코드가 너무 흐트러질 수 있기 때문입니다.

```javascript
// 700ms라는 수는 UX A/B 테스트 결과에 기초하여 경험적으로 계산된 것입니다.
// @보세요: <실험 또는 JIRA 작업에 관련된 것 또는 숫자 700에 대해 상세히 설명하는 것에 대한 링크>
const callbackDebounceRate = 700;
```

### 💩 항상 자신의 모국어로 주석을 작성하기

만일 "주석 없음"의 원칙을 위반했다면 적어도 주석은 코드 작성에 사용하는 언어와 다른 언어로 작성하세요. 만일 여러분의 모국어가 영어라면 여러분은 이 원칙을 위반해도 괜찮습니다.

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

### 💩 가능한 많이 서식 스타일을 혼합하기

다양성을 축하합시다.

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

### 💩 가능한 많이 한 줄에 코드 입력하기

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

### 💩 조용히 실패하기

오류가 발생할 때마다 다른 사람이 그 오류를 알 필요는 없습니다. 로그도 없고, 오류 모달도 없이, 싸늘하게.

_Good 👍🏻_

```javascript
try {
  // 무언가 예견 불가능한 것.
} catch (error) {
  // 쉿... 🤫
}
```

_Bad 👎🏻_

```javascript
try {
  // 무언가 예견 불가능한 것.
} catch (error) {
  setErrorMessage(error.message);
  // and/or
  logError(error);
}
```

### 💩 전역 변수를 광범위하게 사용하기

세계적인 원칙입니다.

_Good 👍🏻_

```javascript
let x = 5;

function square() {
  x = x ** 2;
}

square(); // 이제 x는 25입니다.
```

_Bad 👎🏻_

```javascript
let x = 5;

function square(num) {
  return num ** 2;
}

x = square(x); // 이제 x는 25입니다.
```

### 💩 사용하지 않을 변수 만들기

혹시 모르니까요.

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

### 💩 가능한 언어라면 타입지정 및/또는 타입검사 하지 않기

_Good 👍🏻_

```javascript
function sum(a, b) {
  return a + b;
}

// 형식이 없으면 신이 나요.
const guessWhat = sum([], {}); // -> "[object Object]"
const guessWhatAgain = sum({}, []); // -> 0
```

_Bad 👎🏻_

```javascript
function sum(a: number, b: number): ?number {
  // 자바스크립트에서 반환 및/또는 타입검사를 하지 않은 경우를 커버하는 조건
  if (typeof a !== 'number' && typeof b !== 'number') {
    return undefined;
  }
  return a + b;
}
// 이 경우는 반환/컴파일의 경우에 실패할 것입니다.
const guessWhat = sum([], {}); // -> undefined
```

### 💩 연결할 수 없는 코드 작성하기

이 것이 여러분의 "플랜 B" 입니다.

_Good 👍🏻_

```javascript
function square(num) {
  if (typeof num === 'undefined') {
    return undefined;
  }
  else {
    return num ** 2;
  }
  return null; // 이 것이 나의 "플랜 B".
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

### 💩 삼각형 규칙

새처럼 되자 - 둥지를 틀자, 둥지를 틀자, 둥지를 틀자.

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

### 💩 들여쓰기 망치기

들여쓰기는 에디터에서 복잡한 코드의 공간을 더 차지하기 때문에 들여쓰기를 피합시다. 만약 피하고 싶지 않다면 그냥 그들을 엉망으로 가지고 노세요.

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

### 💩 dependencies 잠그지 않기 

새로운 설치가 있을 때마다 제어되지 않는 방식으로 dependencies를 업데이트 하세요. 왜 과거에 집착하죠, 최첨단 라이브러리 버전을 사용합시다.

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

### 💩 항상 boolean 타입 변수의 이름을 'flag'로 만들기

boolean 값이 무엇을 의미하는지 동료들이 생각할 공간을 남겨둡시다.

_Good 👍🏻_

```javascript
let flag = true;
```

_Bad 👎🏻_

```javascript
let isDone = false;
let isEmpty = false;
```

### 💩 길게 쓰인 function들이 짧은 것보다 낫다.

프로그램 로직을 읽을 수 있는 조각으로 나누지 맙시다. 만일 여러분이 사용하는 IDE의 검색이 중단되고 필수적인 파일 또는 function을 찾을 수 없다면 어떻게 하겠습니까?

- 한 개의 파일에 10000 줄의 코드가 있어도 괜찮습니다.
- 한 개의 function에 1000 줄의 코드가 있어도 괜찮습니다.
- 많은 서비스들 (써드파티와 내부기능, 몇몇 헬퍼들, ORM과 jQuery slider로 직접 작성된 자료들 ) 이 `service.js` 하나에 들어있다구요? 괜찮습니다.

### 💩 작성한 코드를 테스트 해보는 것을 피하기

이 것은 중복되고 불필요한 일의 양입니다.

### 💩 최대한 code linter들을 피하려고 노력하기

특히 둘 이상의 개발자가 있는 팀인 경우 원하는 대로 코드를 작성합니다. 이것은 '자유'의 규칙입니다.

### 💩 README 파일이 없이 프로젝트 시작하기

그리고 당분간은 그렇게 지내세요.

### 💩 불필요한 코드가 필요합니다

어플에서 사용하지 않는 코드를 삭제하지 마세요. 기껏해야, 주석정도 입니다.
