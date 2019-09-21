# JS summary 2018-2019 Uhasselt
Created by Ingo Andelhofs  
Student at Uhasselt

## Introduction
Javascript zorgt voor interactie met de DOM. Je kan scripts zowel inline/document-level als extern koppelen aan je html file. We verkiezen natuurlijk extern onderaan het html bestand. Hierdoor is alle html al gerenderd.   

Javascript kan gebruikt worden voor:
- HTML/CSS aan te passen.
- Communicatie met de server.
- Data opslaan. (cookies aanpassen, local storage, ...)

## Syntax
### Functions
```js
function aFunction() {
    // Code here ...   
}
```

### Variables and constants
```js
const aConstant = 'const';
let aVariable = 'local';
var anotherVaribale = 'global and local depending on the location';
```

### Types
In js heb je alle bekende types zoals int, char, string, float, bool, array, ... Deze moet je zelf niet aanduiden maar je kan ze gewoon gelijk stellen aan bv. `let a = 10;` gevolgd door `a = 'hello';`. Enkele speciale waardes zijn `undefined` geen waarde, `null` leeg, `NaN` not a number.   
Als je met meerdere types werkt is het vaak beter om eerst de casten naar een type. Anders gebeurt dit door Js zelf.

### Objects
Alles in javascript is een object. Je kan bepaalde properties dus accessen via de gekende `.` notation. Ook kan je je eigen class aanmaken in Js.
```js
// Classes
class MyClass {
    constructor(){
        // Init
    }

    aMethod() {
        // Code here...
    }
}

// Objects
let obj = {
    property = 'value',
    anArray = [1, 2, 3]
};
```

### Arrays
Bij js arrays moet je index geen nummer zijn. Dit kan ook een value zijn waardoor je assoc arrays kan maken.
```js
let normalArray = [0, 'hello', true];

let assocArray = [];
assocArray['key'] = 'value';

// Enkele methods
// - sort()
// - pop()
// - push()
// - unshift()
// - join()
// ...
``` 

## The DOM
```js
let header = document.getElementById('header');
if (header !== null) {
    ...
}

// Alternatives
document.querySelector('p.class-name #id-name');
document.querySelectorAll('p.class-name #id-name');
document.getElementsByTagName('p');
document.getElementsByClassName('header');

// Further
element.parentNode();
element.previousSibling();
element.nextSibling();
element.firstChild();
element.lastChild();

element.createElement();
element.createTextNode();
element.appendChild();
element.removeChild();

element.hasAttribute(name);
element.getAttribute(name);
element.removeAttribute(name);
element.setAttribute(name, value);

element.innerHTML = '<tag>content</tag>';

// Event listeners
element.addEventListener('click', e => {
    // Code here ...
}, false);
element.removeEventListener();
```

## Forms
In javascript kan je ook met eventlisteners aan form validation doen voor te controleren op bv. lege velden, ... Aan de serverside moet je dan nog controleren op data in de database. In je event listener van je submit button kan je gebruik maken van `e.preventDefault();`

### HTML5 form validation
- min, max
- minlength, maxlength
- pattern

## The console
Je kan tijdens development ook data naar de console schrijven via `console.log(...)` of `console.error()`.