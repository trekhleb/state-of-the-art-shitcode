# A legkorszerűbb foskód alapelvei

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

Az alábbi lista a legkorszerűbb foskód alapelveit sorakoztatja fel, amiket a projektednek követni kell ahhoz,
hogy valódi foskódnak nevezhesd.

_Ez a dokumentum elérhető a következő nyelveken is:_
[_English_](README.md),
[_简体中文_](README.zh-CN.md),
[_한국어_](README.ko-KR.md)

## Szerezd meg a jelvényed

Ha az adattárad követi a legkorszerűbb foskód alapelveit, akkor használhatod ezt a "state-of-the-art shitcode" jelvényt:

[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)

A jelvény markdown forráskódja:

```
[![State-of-the-art Shitcode](https://img.shields.io/static/v1?label=State-of-the-art&message=Shitcode&color=7B5804)](https://github.com/trekhleb/state-of-the-art-shitcode)
```

## Az alapelvek

### 💩 A változóknak olyan neveket adj, mintha azok már obfuszkálva lennének

Kevesebb billentyűleütés, több szabadidő neked.

_Jó 👍🏻_

```javascript
let a = 42;
```

_Rossz 👎🏻_

```javascript
let age = 42;
```

### 💩 Használd vegyesen a változó/függvény elnevezési konvenciókat

Ünnepeld a különbözőséget!

_Jó 👍🏻_

```javascript
let wWidth = 640;
let w_height = 480;
```

_Rossz 👎🏻_

```javascript
let windowWidth = 640;
let windowHeight = 480;
```

### 💩 Soha ne írj kommentet

Amúgy se fogja senki elolvasni a kódodat.

_Jó 👍🏻_

```javascript
const cdr = 700;
```

_Rossz 👎🏻_

Gyakran a kommenteknek tartalmazniuk kellene a "miértet" és nem azt, hogy "mit" csinál a kód. Ha a "mit" nem tiszta a kód alapján,
akkor a kód valószínűleg túl zavaros.

```javascript
// A 700 milliszekundum érték empirikus módszerrel lett kiszámítva UX A/B teszteredmények alapján.
// @see: <hivatkozás a kísérletre, kapcsolódó JIRA jegyre vagy bármi másra, ami részletes magyaráztatot ad a 700-as értékre>
const callbackDebounceRate = 700;
```

### 💩 A kommenteket mindig az anyanyelveden írd

Ha megszegted a "semmi kommentelés" elvét, akkor legalább olyan nyelven írd, ami eltér attól a nyelvtől, amiben a kódot írod.
Ha angol az anyanyelved, akkor megszegedheted ezt a szabályt.

_Jó 👍🏻_

```javascript
// A modális ablak bezárásra kerül a fizetés teljesítése után.
toggleModal(false);
```

_Rossz 👎🏻_

```javascript
// Hide modal window on error.
toggleModal(false);
```

### 💩 A lehető legjobban próbáld keverni a formázási stílusokat

Ünnepeld a különbözőséget!

_Jó 👍🏻_

```javascript
let i = ['tomato', 'onion', 'mushrooms'];
let d = [ "ketchup", "mayonnaise" ];
```

_Rossz 👎🏻_

```javascript
let ingredients = ['tomato', 'onion', 'mushrooms'];
let dressings = ['ketchup', 'mayonnaise'];
```

### 💩 Helyezd a lehető legtöbb kódot egyetlen sorba

_Jó 👍🏻_

```javascript
document.location.search.replace(/(^\?)/,'').split('&').reduce(function(o,n){n=n.split('=');o[n[0]]=n[1];return o},{})
```

_Rossz 👎🏻_

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

### 💩 A kódod csendben haljon meg

Amikor hibába futsz, nem kell, hogy bárki is tudjon róla. Semmi naplózás, semmi hibaablak, ne parázz.

_Jó 👍🏻_

```javascript
try {
  // Kódrészlet, ami váratlanul félremegy.
} catch (error) {
  // psszt... 🤫
}
```

_Rossz 👎🏻_

```javascript
try {
  // Kódrészlet, ami váratlanul félremegy.
} catch (error) {
  setErrorMessage(error.message);
  // és/vagy
  logError(error);
}
```

### 💩 Használj globális változókat mértéktelen módon

A globalizáció elve.

_Jó 👍🏻_

```javascript
let x = 5;

function square() {
  x = x ** 2;
}

square(); // Az x értéke most már 25.
```

_Rossz 👎🏻_

```javascript
let x = 5;

function square(num) {
  return num ** 2;
}

x = square(x); // Az x értéke most már 25.
```

### 💩 Hozz létre változókat, amiket később nem fogsz használni

Hátha esetleg még szükség lesz rájuk.

_Jó 👍🏻_

```javascript
function sum(a, b, c) {
  const timeout = 1300;
  const result = a + b;
  return a + b;
}
```

_Rossz 👎🏻_

```javascript
function sum(a, b) {
  return a + b;
}
```

### 💩 Ne adj meg típusokat és/vagy ne végezz típusellenőrzést, ha a nyelv megengedi ezt

_Jó 👍🏻_

```javascript
function sum(a, b) {
  return a + b;
}

// Ez itt a típustalan móka helye.
const guessWhat = sum([], {}); // -> "[object Object]"
const guessWhatAgain = sum({}, []); // -> 0
```

_Rossz👎🏻_

```javascript
function sum(a: number, b: number): ?number {
  // Azon eset lefedése, amikor nem végzünk forrás-forrás fordítást és/vagy Flow típusellenőrzést JS-ben.
  if (typeof a !== 'number' && typeof b !== 'number') {
    return undefined;
  }
  return a + b;
}

// Ennek meg kell halnia a fordítás során.
const guessWhat = sum([], {}); // -> undefined
```

### 💩 Mindenképp legyen elérhetetlen kódrész

Ez a te B-terved.

_Jó 👍🏻_

```javascript
function square(num) {
  if (typeof num === 'undefined') {
    return undefined;
  }
  else {
    return num ** 2;
  }
  return null; // Ez az én B-tervem.
}
```

_Rossz 👎🏻_

```javascript
function square(num) {
  if (typeof num === 'undefined') {
    return undefined;
  }
  return num ** 2;
}
```

### 💩 A háromszög elve

Légy olyan, mint a bokszolók - behúzás, behúzás, behúzás.

_Jó 👍🏻_

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

_Rossz 👎🏻_

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

### 💩 Szórakozz az indentálásokkal

Kerüld az indentálásokat, mert így a komplex kód több helyet foglal el a szerkesztőben. Ha nincs kedved elkerülni őket, akkor add meg őket hasraütésszerűen.

_Jó 👍🏻_

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

_Rossz 👎🏻_

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

### 💩 Ne zárold a függőségeidet

Frissítsd a függőségeket minden egyes új telepítés során, ellenőrizetlenül. Minek ragaszkodnál a múlthoz?!
Használd a könyvtárak legújabb, legkorszerűbb verzióit.

_Jó 👍🏻_

```
$ ls -la

package.json
```

_Rossz 👎🏻_

```
$ ls -la

package.json
package-lock.json
```

### 💩 A boolean értékeket mindig `flag`-nek (jelző) nevezd el

Add meg a lehetőséget a kollégáid számára, hogy kitalálják, mit is jelent az a boolean érték.

_Jó 👍🏻_

```javascript
let flag = true;
```

_Rossz 👎🏻_

```javascript
let isDone = false;
let isEmpty = false;
```

### 💩 A hosszú függvények jobbak a rövideknél

Ne oszd fel a programot olvasható részekre. Mi van, ha az IDE keresője meghibásodik, és nem lesz módod megtalálni a szükséges fájlt vagy függvényt?

- 10000 kódsor egyetlen fájlban - teljesen rendben van.
- 1000 soros függvény - teljesen rendben van.
- Szolgáltatások (harmadik féltől származó és belső, segédfüggvények, kézzel írott adatbázis ORM és jQuery csúszka) kezelése egyetlen `service.js` fájlban? Jó'van az úgy.

### 💩 Kerüld a kódod tesztekkel történő lefedését

Ez egy tök felesleges extra munka.

### 💩 Amennyire csak képes vagy rá, kerüld a kód-linter-eket

Kódolj, ahogy csak akarsz, főleg akkor, ha csapatban dolgozol. Ez a "szabadság" elve.

### 💩 A projekjeidet README fájl nélküld kezdd

És egyelőre ez maradjon is így.

### 💩 Legyenek felesleges kódrészletek

Ne törölj olyan kódot, amit már nem használ az alkalmazásod. Maximum kommenteld ki.
