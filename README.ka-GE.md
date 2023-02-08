# State-of-the-Art Shitcode Principles
# უვარგისი კოდის წერის თანამედროვე პრინციპები

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

This a list of state-of-the-art shitcode principles your project should follow to call it a proper shitcode.
უვარგისი კოდის წერის თანამედროვე პრინციპები, რომლებსაც თქვენი პროექტი აუცილებლად უნდა იცავდეს, რათა მის უვარგისობაში ეჭვი არავის შეეპაროს.

_წინამდებარე დოკუმენტი ასევე ხელმისაწვდომია შემდეგ ენებზე:_
[_English_](README.md),
[_简体中文_](README.zh-CN.md),
[_한국어_](README.ko-KR.md)

## Get Your Badge
## ემბლემა დამსახურებისამებრ

If your repository follows the state-of-the-art shitcode principles you may use the following "state-of-the-art shitcode" badge:
თუკი თქვენს საცავში (_repository_-ში) მკაცრად არის დაცული უვარგისი კოდის წერის პრინციპები, შეგიძლიათ ეს მიღწევა შემდეგი ემბლემის გამოყენებით აღნიშნოთ:

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

Markdown source-code for the badge:
მოცემული ემბლემის გამოსახვისათვის საჭირო კოდი (_Markdown_):

```
[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)
```

## The Principles
## პრინციპები

### 💩 Name variables in a way as if your code was already obfuscated
### 💩 ცვლადებისათვის სახელები ისე შეარჩიეთ, რომ თქვენი კოდი ბუნდოვანი გახდეს

Fewer keystrokes, more time for you.
ნაკლები ბარტყუნი კლავიშებზე, დროის დანაზოგი თქვენთვის.

_კარგია 👍🏻_

```javascript
let a = 42;
```

_ცუდია 👎🏻_

```javascript
let age = 42;
```

### 💩 Mix variable/functions naming style
### 💩 ერთმანეთში აურიეთ ცვლადებისა და ფუნქციების სახელდების სტილი

Celebrate the difference.
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

### 💩 Never write comments
### 💩 არასოდეს დაწეროთ კომენტარები

No one is going to read your code anyway.
თქვენი კოდის წაკითხვას მაინც არავინ აპირებს.

_კარგია 👍🏻_

```javascript
const cdr = 700;
```

_ცუდია 👎🏻_

More often comments should contain some 'why' and not some 'what'. If the 'what' is not clear in the code, the code is probably too messy.
კომენტარები უმეტესწილად უნდა შეიცავდეს „რატომ“-ს და არა „რა“-ს. თუ კოდში „რა“ ბუნდოვანია, მაშასადამე, კოდი მეტისმეტად მოუწესრიგებელია.

```javascript
// The number of 700ms has been calculated empirically based on UX A/B test results.
// @see: <link to experiment or to related JIRA task or to something that explains number 700 in details>
const callbackDebounceRate = 700;
```

### 💩 Always write comments in your native language
### 💩 კომენტარები ყოველთვის წერეთ თქვენს მშობლიურ ენაზე

If you violated the "No comments" principle then at least try to write comments in a language that is different from the language you use to write the code. If your native language is English you may violate this principle.
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

### 💩 Try to mix formatting style as much as possible
### 💩 შეძლებისდაგვარად მაქსიმალურად მოახდინეთ ფორმატირების სტილთა არევ-დარევა

Celebrate the difference.
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

### 💩 Put as much code as possible into one line
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

Whenever you catch an error it is not necessary for anyone to know about it. No logs, no error modals, chill.
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

### 💩 Use global variables extensively
### 💩 ფართოდ გამოიყენეთ გლობალური ცვლადები

Globalization principle.
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

### 💩 Create variables that you're not going to use.
### 💩 შექმენით ცვლადები, რომელთა გამოიყენებასაც არ აპირებთ

Just in case.
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

### 💩 Don't specify types and/or don't do type checks if language allows you to do so.
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

### 💩 You need to have an unreachable piece of code
### 💩 უნდა გაგაჩნდეთ კოდის მიუწვდომელი ნაწილები

This is your "Plan B".
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

### 💩 Triangle principle
### 💩 სამკუთხედის პრინციპი

Be like a bird - nest, nest, nest.
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

### 💩 Mess with indentations
### 💩 აურ-დაურიეთ აბზაცები

Avoid indentations since they make complex code take up more space in the editor. If you're not feeling like avoiding them then just mess with them.
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

### 💩 Do not lock your dependencies
### 💩 ნუ დალუქავთ დაქვემდებარებებს (_dependencies_)

Update your dependencies on each new installation in uncontrolled way. Why stick to the past, let's use the cutting edge libraries versions.
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

### 💩 Always name your boolean value a `flag`
### 💩 ლოგიკური მნიშვნელობის მქონე ცვლადებს ყოველთვის დაარქვით `flag`

Leave the space for your colleagues to think what the boolean value means.
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

### 💩 Long-read functions are better than short ones.
### 💩 გრძლად დაწერილი ფუნქციები უკეთესია, ვიდრე მოკლედ დაწერილი

Don't divide a program logic into readable pieces. What if your IDE's search breaks and you will not be able to find the necessary file or function?
ნუ დაყოფთ პროგრამის ლოგიკას წაკითხვად ფრაგმენტებად. წარმოიდგინეთ, რა შეიძლება მოხდეს, თუკი უეცრად თქვენი IDE-ის ძებნის ფუნქცია მოიშლება და აღარ გექნებათ შესაძლებლობა, მოძებნოთ საჭირო ფაილი თუ ფუნქცია.

- 10000 lines of code in one file is OK.
- 10000 ხაზისაგან შემდგარი კოდის ერთ ფაილში განთავსება ჩვეულებრივი ამბავია.
- 1000 lines of a function body is OK.
- ფუნქციის ტანის 1000 ხაზისაგან შედგენა ჩვეულებრივი ამბავია.
- Dealing with many services (3rd party and internal, also, there are some helpers, database hand-written ORM and jQuery slider) in one `service.js`? It's OK.
- მუშაობთ რამდენიმე სერვისთან (მე-3 მხარის მიერ უზრუნველყოფილთან თუ შიდასთან, ასევე, გაქვთ რამდენიმე დამხმარე ფუნქცია, ნულიდან დაწერილი მონაცემთა ბაზის ORM-ი და jQuery-ის „სლაიდერი“) ერთად-ერთ `service.js`-ში? არაფერია, ჩვეულებრივი ამბავია.

### 💩 Avoid covering your code with tests
### 💩 მოერიდეთ თქვენი კოდის ტესტირებას

This is a duplicate and unnecessary amount of work.
ეს არის ზედმეტი და არასაჭიროდ გაწეული შრომა. 

### 💩 As hard as you can try to avoid code linters
### 💩 რაც შეიძლება ძლიერ ეცადეთ, მოერიდოთ კოდის linter-ებს

Write code as you want, especially if there is more than one developer in a team. This is a "freedom" principle.
წერეთ კოდი ისე, როგორც თქვენ გინდათ, განსაკუთრებით მაშინ, როცა გუნდი არაერთი დეველოპერისგან შედგება. ეს გახლავთ „თავისუფლების“ პრინციპი.

### 💩 Start your project without a README file.
### 💩 წამოიწყეთ პროექტი README ფაილის გარეშე

And keep it that way for the time being.
და ჯერჯერობით ასე დატოვეთ.

### 💩 You need to have unnecessary code
### 💩 უნდა გაგაჩნდეთ არასაჭირო კოდი

Don't delete the code your app doesn't use. At most, comment it.
არ წაშალოთ კოდი, რომელსაც თქვენი აპლიკაცია არ იყენებს. დიდი-დიდი, დააკომენტარეთ.
