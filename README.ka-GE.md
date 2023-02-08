# უვარგისი კოდის წერის თანამედროვე პრინციპები

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

უვარგისი კოდის წერის თანამედროვე პრინციპები, რომლებსაც თქვენი პროექტი აუცილებლად უნდა იცავდეს, რათა მის უვარგისობაში ეჭვი არავის შეეპაროს.

_წინამდებარე დოკუმენტი ასევე ხელმისაწვდომია შემდეგ ენებზე:_
[_English_](README.md),
[_简体中文_](README.zh-CN.md),
[_한국어_](README.ko-KR.md)

## ემბლემა დამსახურებისამებრ

თუკი თქვენს საცავში (_repository_-ში) მკაცრად არის დაცული უვარგისი კოდის წერის პრინციპები, შეგიძლიათ ეს მიღწევა შემდეგი ემბლემის გამოყენებით აღნიშნოთ:

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

მოცემული ემბლემის გამოსახვისათვის საჭირო კოდი (_Markdown_):

```
[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)
```

## პრინციპები

### 💩 ცვლადებისათვის სახელები ისე შეარჩიეთ, რომ თქვენი კოდი ბუნდოვანი გახდეს

ნაკლები ბარტყუნი კლავიშებზე, დროის დანაზოგი თქვენთვის.

_კარგია 👍🏻_

```javascript
let a = 42;
```

_ცუდია 👎🏻_

```javascript
let age = 42;
```

### 💩 ერთმანეთში აურიეთ ცვლადებისა და ფუნქციების სახელდების სტილი

დიდება მრავალფეროვნებას!

_კარგია 👍🏻_

```javascript
let wWidth = 640;
let w_height = 480;
```

_ცუდია 👎🏻_

```javascript
let windowWidth = 640;
let windowHeight = 480;
```

### 💩 არასოდეს დაწეროთ კომენტარები

თქვენი კოდის წაკითხვას მაინც არავინ აპირებს.

_კარგია 👍🏻_

```javascript
const cdr = 700;
```

_ცუდია 👎🏻_

კომენტარები უმეტესწილად უნდა შეიცავდეს „რატომ“-ს და არა „რა“-ს. თუ კოდში „რა“ ბუნდოვანია, მაშასადამე, კოდი მეტისმეტად მოუწესრიგებელია.

```javascript
// The number of 700ms has been calculated empirically based on UX A/B test results.
// @see: <link to experiment or to related JIRA task or to something that explains number 700 in details>
const callbackDebounceRate = 700;
```

### 💩 კომენტარები ყოველთვის წერეთ თქვენს მშობლიურ ენაზე

თუკი უგულებელყოფთ პრინციპს „კომენტარების გარეშე“, მაშინ კომენტარები ისეთ ენაზე მაინც დაწერეთ, რომელიც განსხვავებული იქნება იმ ენისაგან, რომელსაც კოდის საწერად იყენებთ. თუ თქვენი მშობლიეური ენა არის ინგლისური, შეგიძლიათ მოცემული პრინციპი უგულებელყოთ.

_კარგია 👍🏻_

```javascript
// Закриваємо модальне віконечко при виникненні помилки.
toggleModal(false);
```

_ცუდია 👎🏻_

```javascript
// Hide modal window on error.
toggleModal(false);
```

### 💩 შეძლებისდაგვარად მაქსიმალურად მოახდინეთ ფორმატირების სტილთა არევ-დარევა

დიდება მრავალფეროვნებას!

_კარგია 👍🏻_

```javascript
let i = ['tomato', 'onion', 'mushrooms'];
let d = [ "ketchup", "mayonnaise" ];
```

_ცუდია 👎🏻_

```javascript
let ingredients = ['tomato', 'onion', 'mushrooms'];
let dressings = ['ketchup', 'mayonnaise'];
```

### 💩 განათავსეთ რაც შეიძლება მეტი კოდი ერთ ხაზზე

_კარგია 👍🏻_

```javascript
document.location.search.replace(/(^\?)/,'').split('&').reduce(function(o,n){n=n.split('=');o[n[0]]=n[1];return o},{})
```

_ცუდია 👎🏻_

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

### 💩 კრახი უჩუმრად განიცადეთ

როდესაც რაიმე შეცდომას აღმოაჩენთ, არ არის საჭირო, ამის შესახებ ვინმემ რამე იცოდეს. არანაირი აღრიცხვა, არანაირი შეტყობინებები შეცდომის შესახებ, მოდუნდით.

_კარგია 👍🏻_

```javascript
try {
  // რაღაც არაპროგნოზირებადი.
} catch (error) {
  // ჩშშ... 🤫
}
```

_ცუდია 👎🏻_

```javascript
try {
  // რაღაც არაპროგნოზირებადი.
} catch (error) {
  setErrorMessage(error.message);
  // ან/და
  logError(error);
}
```

### 💩 ფართოდ გამოიყენეთ გლობალური ცვლადები

გლობალიზაციის პრინციპი.

_კარგია 👍🏻_

```javascript
let x = 5;

function square() {
  x = x ** 2;
}

square(); // ახლა x არის 25.
```

_ცუდია 👎🏻_

```javascript
let x = 5;

function square(num) {
  return num ** 2;
}

x = square(x); // ახლა x არის 25.
```

### 💩 შექმენით ცვლადები, რომელთა გამოიყენებასაც არ აპირებთ

ყოველი შემთხვევისთვის.

_კარგია 👍🏻_

```javascript
function sum(a, b, c) {
  const timeout = 1300;
  const result = a + b;
  return a + b;
}
```

_ცუდია 👎🏻_

```javascript
function sum(a, b) {
  return a + b;
}
```

### 💩 შეძლებისდაგვარად მოერიდეთ ტიპების განსაზღვრას ან/და ტიპების შემოწმებას იმ ენებში, სადაც ამის საშუალება გაქვთ

_კარგია 👍🏻_

```javascript
function sum(a, b) {
  return a + b;
}

// ისიამოვნეთ უტიპებოდ.
const guessWhat = sum([], {}); // -> "[object Object]"
const guessWhatAgain = sum({}, []); // -> 0
```

_ცუდია 👎🏻_

```javascript
function sum(a: number, b: number): ?number {
  // აშუქებს შემთხვევას, როცა ჩვენ არ ვახდენთ ტრანსპილაციას ან/და Flow-ს გამოყენებით ტიპების შემოწმებას JS-ში.
  if (typeof a !== 'number' && typeof b !== 'number') {
    return undefined;
  }
  return a + b;
}

// ამან მარცხი უნდა განიცადოს ტრანსპილაციის/კომპილაციის პროცესში.
const guessWhat = sum([], {}); // -> undefined
```

### 💩 უნდა გაგაჩნდეთ კოდის მიუწვდომელი ნაწილები

ეს არის თქვენი „გეგმა B“.

_კარგია 👍🏻_

```javascript
function square(num) {
  if (typeof num === 'undefined') {
    return undefined;
  }
  else {
    return num ** 2;
  }
  return null; // ეს არის ჩემი „გეგმა B“..
}
```

_ცუდია 👎🏻_

```javascript
function square(num) {
  if (typeof num === 'undefined') {
    return undefined;
  }
  return num ** 2;
}
```

### 💩 სამკუთხედის პრინციპი

მიბაძეთ ჩიტებს — დაიბუდეთ, დაიბუდეთ, დაიბუდეთ.

_კარგია 👍🏻_

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

_ცუდია 👎🏻_

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

### 💩 აურ-დაურიეთ აბზაცები

მოერიდეთ აბზაცებს, რადგან ისინი ქმნიან კომპლექსურ კოდს, რომელიც მეტ სივრცეს იკავებს რედაქტორში. თუ არ გსურთ მოერიდოთ მათ, მაშინ ადექით და მათში უწესრიგობა შეიტანეთ.

_კარგია 👍🏻_

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

_ცუდია 👎🏻_

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

### 💩 ნუ დალუქავთ დაქვემდებარებებს (_dependencies_)

განაახლეთ თქვენი დაქვემდებარებები ყოველი ახალი ინსტალაციისას უკონტროლოდ. რატომ ჩავრჩეთ წარსულში, მოდი, გამოვიყენოთ ბიბლიოთეკების უახლესი (არასტაბილური) ვერსიები.

_კარგია 👍🏻_

```
$ ls -la

package.json
```

_ცუდია 👎🏻_

```
$ ls -la

package.json
package-lock.json
```

### 💩 ლოგიკური მნიშვნელობის მქონე ცვლადებს ყოველთვის დაარქვით `flag`

მიეცით გასაქანი თქვენს კოლეგებს, დაე იფიქრონ, რას შეიძლება წარმოადგენდეს ეს ლოგიკური მნიშვნელობა.

_კარგია 👍🏻_

```javascript
let flag = true;
```

_ცუდია 👎🏻_

```javascript
let isDone = false;
let isEmpty = false;
```

### 💩 გრძლად დაწერილი ფუნქციები უკეთესია, ვიდრე მოკლედ დაწერილი

ნუ დაყოფთ პროგრამის ლოგიკას წაკითხვად ფრაგმენტებად. წარმოიდგინეთ, რა შეიძლება მოხდეს, თუკი უეცრად თქვენი IDE-ის ძებნის ფუნქცია მოიშლება და აღარ გექნებათ შესაძლებლობა, მოძებნოთ საჭირო ფაილი თუ ფუნქცია.

- 10000 ხაზისაგან შემდგარი კოდის ერთ ფაილში განთავსება ჩვეულებრივი ამბავია.
- ფუნქციის ტანის 1000 ხაზისაგან შედგენა ჩვეულებრივი ამბავია.
- მუშაობთ რამდენიმე სერვისთან (მე-3 მხარის მიერ უზრუნველყოფილთან თუ შიდასთან, ასევე, გაქვთ რამდენიმე დამხმარე ფუნქცია, ნულიდან დაწერილი მონაცემთა ბაზის ORM-ი და jQuery-ის „სლაიდერი“) ერთად-ერთ `service.js`-ში? არაფერია, ჩვეულებრივი ამბავია.

### 💩 მოერიდეთ თქვენი კოდის ტესტირებას

ეს არის ზედმეტი და არასაჭიროდ გაწეული შრომა. 

### 💩 რაც შეიძლება ძლიერ ეცადეთ, მოერიდოთ კოდის linter-ებს

წერეთ კოდი ისე, როგორც თქვენ გინდათ, განსაკუთრებით მაშინ, როცა გუნდი არაერთი დეველოპერისგან შედგება. ეს გახლავთ „თავისუფლების“ პრინციპი.

### 💩 წამოიწყეთ პროექტი README ფაილის გარეშე

და ჯერჯერობით ასე დატოვეთ.

### 💩 უნდა გაგაჩნდეთ არასაჭირო კოდი

არ წაშალოთ კოდი, რომელსაც თქვენი აპლიკაცია არ იყენებს. დიდი-დიდი, დააკომენტარეთ.
