#  Принципы передового дерьмокода

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

Здесь представлен список передовых принципов написания дерьмокода, при соблюдении которых ваш проект можно спокойно называть дерьмокодом.

_Читайте на других языках:_
[_English_](README.md),
[_简体中文_](README.zh-CN.md),
[_한국어_](README.ko-KR.md)

## Получи значок

Если ваш репозиторий соответствует нижеописанным принципам, то можете добавить соответствующий значок:

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

Код Markdown для значка:

```
[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)
```

## Принципы

### 💩 Называй переменные будто твой код уже обфусцирован

Меньше нажатий на клавиши — больше личного времени.

_Хорошо 👍🏻_

```javascript
let a = 42;
```

_Плохо 👎🏻_

```javascript
let age = 42;
```

### 💩 Смешивай стиль именования переменных/функций

Радуйся разнообразию.

_Хорошо 👍🏻_

```javascript
let wWidth = 640;
let w_height = 480;
```

_Плохо 👎🏻_

```javascript
let windowWidth = 640;
let windowHeight = 480;
```

### 💩 Никогда не пиши комментарии

Все равно никто не будет читать твой код.

_Хорошо 👍🏻_

```javascript
const cdr = 700;
```

_Плохо 👎🏻_

Комментарии чаще всего должны говорить "почему?" а не "как?". Если "как?" по коду не понятно, то, вероятно, код слишком запутан. 

```javascript
// Константа в 700ms эмпирически подобрана на основе результатов UX A/B тестов.
// @see: <ссылка на эксперимент, на связанную таску в JIRA, или что-то детально объясняющее почему тут используется именно число 700>
const callbackDebounceRate = 700;
```

### 💩 Всегда пиши комментарий на родном языке

Если нарушаешь принцип "Без комментариев", то хотя бы постарайся писать комментарии на языке отличном от используемого при написании кода. Если твой родной язык английский, то можешь нарушать этот принцип.

_Хорошо 👍🏻_

```javascript
// Закриваємо модальне віконечко при виникненні помилки.
toggleModal(false);
```

_Плохо 👎🏻_

```javascript
// Hide modal window on error.
toggleModal(false);
```

### 💩 Старайся смешивать стили форматирования как можно чаще

Радуйся разнообразию.

_Хорошо 👍🏻_

```javascript
let i = ['tomato', 'onion', 'mushrooms'];
let d = [ "ketchup", "mayonnaise" ];
```

_Плохо 👎🏻_

```javascript
let ingredients = ['tomato', 'onion', 'mushrooms'];
let dressings = ['ketchup', 'mayonnaise'];
```

### 💩 Пихай как можно больше кода в одну строчку

_Хорошо 👍🏻_

```javascript
document.location.search.replace(/(^\?)/,'').split('&').reduce(function(o,n){n=n.split('=');o[n[0]]=n[1];return o},{})
```

_Плохо 👎🏻_

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

### 💩 Падай тихо

Если поймал исключение, то никто не должен об этом знать. Никаких логов, никаких всплывающих окон, одно спокойствие.

_Хорошо 👍🏻_

```javascript
try {
  // Что-то непредвиденное.
} catch (error) {
  // Тссс... 🤫
}
```

_Плохо 👎🏻_

```javascript
try {
  // Что-то непредвиденное.
} catch (error) {
  setErrorMessage(error.message);
  // и/или
  logError(error);
}
```

### 💩 Используй глобальные  переменные на широкую ногу

Принцип глобализации.

_Хорошо 👍🏻_

```javascript
let x = 5;

function square() {
  x = x ** 2;
}

square(); // Теперь x равен 25.
```

_Плохо 👎🏻_

```javascript
let x = 5;

function square(num) {
  return num ** 2;
}

x = square(x); // Теперь x равен 25.
```

### 💩 Создавай неиспользуемые переменные.

Просто на всякий случай.

_Хорошо 👍🏻_

```javascript
function sum(a, b, c) {
  const timeout = 1300;
  const result = a + b;
  return a + b;
}
```

_Плохо 👎🏻_

```javascript
function sum(a, b) {
  return a + b;
}
```

### 💩 Не указывай типы и/или проверки типов когда используемый язык программирования это позволяет.

_Хорошо 👍🏻_

```javascript
function sum(a, b) {
  return a + b;
}

// Нетипизированное веселье творится здесь.
const guessWhat = sum([], {}); // -> "[object Object]"
const guessWhatAgain = sum({}, []); // -> 0
```

_Плохо 👎🏻_

```javascript
function sum(a: number, b: number): ?number {
  // Покрытие ситуации, когда не используем транспиляцию и/или чекеры типа Flow в JS
  if (typeof a !== 'number' && typeof b !== 'number') {
    return undefined;
  }
  return a + b;
}

// Должно упасть при транспиляции/компиляции
const guessWhat = sum([], {}); // -> undefined
```

### 💩 Недостижимый код нужен

Это твой "План Б".

_Хорошо 👍🏻_

```javascript
function square(num) {
  if (typeof num === 'undefined') {
    return undefined;
  }
  else {
    return num ** 2;
  }
  return null; // Это мой "План Б".
}
```

_Плохо 👎🏻_

```javascript
function square(num) {
  if (typeof num === 'undefined') {
    return undefined;
  }
  return num ** 2;
}
```

### 💩 Принцип треугольника

Будь как матрешка — вложение, вложение, вложение.

_Хорошо 👍🏻_

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

_Плохо 👎🏻_

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

### 💩 Чехарда с отступами

Избегай отступов — из-за них сложный код занимает больше места в редакторе. Ну а если не хочешь, то хотя бы расставляй их убого.

_Хорошо 👍🏻_

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

_Плохо 👎🏻_

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

### 💩 Не блокируй версии зависимостей

Бесконтрольно обновляй зависимости при каждой новой установке. Надо новейшие версии библиотек использовать, а не прошлое держать.

_Хорошо 👍🏻_

```
$ ls -la

package.json
```

_Плохо 👎🏻_

```
$ ls -la

package.json
package-lock.json
```

### 💩 Булевы переменные всегда называй `flag`

Позволь коллегам угадать что же это булево значение означает.

_Хорошо 👍🏻_

```javascript
let flag = true;
```

_Плохо 👎🏻_

```javascript
let isDone = false;
let isEmpty = false;
```

### 💩 Функции-портянки лучше коротких.

Не дели логику на легко воспринимаемые кусочки. Вдруг поиск в IDE внезапно сломается, и тыф не сможешь найти нужный файл или функцию?

- 10000 строк в файле — ЭТО НОРМА.
- 1000 строк в функции — ЭТО НОРМА.
- Работа с кучей сервисов (внутренними и внешними, а еще за компанию кучка хелперов, вручную написанная ORM, ну и слайдер на jQuery) в одном файле `service.js`? ЭТО НОРМА.

### 💩 Не покрывай код тестами

Это дублирование функционеала и бесполезная куча работы.

### 💩 Насколько возможноm, избегай статических анализаторов.

Пиши код как хочется, особенно если ты не единственный разработчик в команде. Таков принцип "свободы".

### 💩 Начни проект без файла README.

И никогда не добавляй его.

### 💩 Бесполезный код нужен

Не удаляй код, который уже не используется в приложении. Закомментируй его хотя бы.
