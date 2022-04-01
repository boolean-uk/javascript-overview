# An Overview of Javascript

This overview was inspired by [Learn X in Y minutes, Where X=javascript](https://learnxinyminutes.com/docs/javascript/).

## Table of Contents

- [Comments](#comments)
- [Numbers, Strings and Operators](#numbers-strings-and-operators)
- [Variables, Arrays and Objects](#variables-arrays-and-objects)
- [Logic and Control Structures](#logic-and-control-structures)
- [Functions, Scope and Closures](#functions-scope-and-closures)
- [More About Objects](#more-about-objects)
- [Constructors and Prototypes](#constructors-and-prototypes)
- [Classes](#classes)

## Comments

```js
// Single-line comments start with two slashes.

/* Multiline comments start with slash-star,
and end with star-slash */

/**
* This doc' uses the common convention of starting multi-line comments with slash-star-star
* Then the comments themselves are on lines beginning with star
* And the last line ends with star-star-slash
**/

// Statements can be terminated by `;`
doStuff();

// But not necessarily, as semicolons are normally inserted automatically wherever there's a newline
doStuff()
```

## Numbers, Strings and Operators

```js
/**
* JavaScript has one number type (which is a 64-bit IEEE 754 double).
* Doubles have a 52-bit mantissa, which is enough to store integers
* up to about 9✕10¹⁵.
**/
3; // = 3
1.5; // = 1.5

// Some basic arithmetic works as you'd expect.
1 + 1; // = 2
8 - 1; // = 7
10 * 2; // = 20
35 / 5; // = 7

// Including uneven division.
5 / 2; // = 2.5

// And modulo division.
10 % 2; // = 0
30 % 4; // = 2
18.5 % 7; // = 4.5

// But because of floating point precision, some arithmetic expressions might not do what you expect
0.1 + 0.2; // = 0.30000000000000004

/**
* Bitwise operations also work; when you perform a bitwise operation your float
* is converted to a signed int *up to* 32 bits.
**/
1 << 2; // 4, because this is a shift left 2 places in base 2, hence 2⁰ becomes 2² = 4

// Precedence is enforced with parentheses.
(1 + 3) * 2; // = 8

// There are three special not-a-real-number values:
Infinity; // result of e.g. 1/0
-Infinity; // result of e.g. -1/0
NaN; // result of e.g. 0/0, stands for 'Not a Number'

// There's also a boolean type.
true;
false;

// Strings are created with `'` or `"`.
'abc';
"Hello, world";

// Negation uses the `!` symbol
!true; // = false
!false; // = true

// Equality is `===`
1 === 1; // = true
2 === 1; // = false

// Inequality is `!==`
1 !== 1; // = false
2 !== 1; // = true

// More comparisons
1 < 10; // = true
1 > 10; // = false
2 <= 2; // = true
2 >= 2; // = true

// Strings are concatenated with `+`
"Hello " + "world!"; // = "Hello world!"

// ... which works with more than just strings
"1, 2, " + 3; // = "1, 2, 3"
"Hello " + ["world", "!"]; // = "Hello world,!"

// and are compared with `<` and `>`
"a" < "b"; // = true

// Type coercion is performed for comparisons with double equals...
"5" == 5; // = true
null == undefined; // = true

// ...unless you use `===`
"5" === 5; // = false
null === undefined; // = false

// ...which can result in some weird behaviour (hence, always use `===`)
13 + !0; // 14
"13" + !0; // '13true'

// You can access characters in a string with `charAt`
"This is a string".charAt(0);  // = 'T'

// ...or use `substring` to get larger pieces.
"Hello world".substring(0, 5); // = "Hello"

// `length` is a property, so don't use ().
"Hello".length; // = 5

// There's also `null` and `undefined`.
null;      // used to indicate a deliberate non-value
undefined; // used to indicate a value is not currently present (although
           // `undefined` is actually a value itself)

/**
* `false`, `null`, `undefined`, `NaN`, `0` and `""` are falsy; everything else is truthy
* Note that `0` is falsy and "0" is truthy, even though `0` == "0".
**/
```

## Variables, Arrays and Objects

```js
/**
* Variables are declared with the `let` or `const` keyword.
* There used to be `var`, too, but declaring variables using `var` is no longer recommended,
* as it places variables in the global scope.
* JavaScript is dynamically typed, so you don't need to specify type.
* Assignment uses a single `=` character.
**/

//`let` variables can be reassigned and are only available in the local lexical scope
let someVar = 5;
someVar = 10;

// `const` variables cannot be reasigned
const author = "Steve";
author = "Billy" // you can't do this

/**
* However, `const` does not mean the value it holds is immutable — just that the variable identifier
* cannot be reassigned. This has implications for arrays and objects, because it means the object's
* contents can be altered. Hence, it is often correct to declare an array or an object `const`,
* even when the contents themselves might change
**/
const myArray = ["Steve", "Andy", "James"];
myArray[2] = "Nathan" // you can do this - ["Steve", "Andy", "Nathan"];

// If you leave the `let` (or `const`) keyword off, you won't necessarily get an error...
someOtherVar = 10;

// ...but your variable will be created in the global scope (which is probably not what you want)

// Variables declared without being assigned to are set to `undefined`.
let someOtherVar; // = undefined

// If you want to declare a couple of variables, then you could use a comma separator
let someThirdVar = 2, someFourthVar = 4;

// There's shorthand for performing math operations on variables:
someVar += 10; // equivalent to someVar = someVar + 10; someVar is 20 now
someVar *= 10; // now someVar is 200

// and an even-shorter-hand for adding or subtracting 1
someVar++; // now someVar is 201
someVar--; // back to 200

// Arrays are ordered lists of values of any type.
const myArray = ["Hello", 45, true];

/**
* Their members can be accessed using the square-brackets subscript syntax.
* Array indices start at zero (unfortunately).
**/
myArray[1]; // = 45

// Arrays are mutable and of variable length.
myArray.push("World");
myArray.length; // = 4

// Add/Modify at specific index
myArray[3] = "Hello";

// Add and remove element from front or back end of an array
myArray.unshift(3); // Add as the first element
someVar = myArray.shift(); // Remove first element and return it
myArray.push(3); // Add as the last element
someVar = myArray.pop(); // Remove last element and return it

// Create a string that joins all elements of an array with a comma (or any other specified symbol)
const myArray0 = [32,false,"js",12,56,90];
myArray0.join(","); // = "32,false,js,12,56,90"

// Get a new array containing elements from an existing array at index 1 (include) to 4 (exclude)
myArray0.slice(1,4); // = [false,"js",12]

/**
* Remove 4 elements from array, starting from index 2
**/
myArray0.splice(2,4); // = ["js",12,56,90]

/**
* JavaScript's objects are equivalent to "dictionaries" or "maps" in other languages
* They are an unordered collection of key-value pairs.
**/
const myObj = {key1: "Hello", key2: "World"};

/**
* Object keys are strings, but quotes aren't required if they're a valid
* JavaScript identifier. Values can be any type.
**/
const myObj = {myKey: "myValue", "my other key": 4};

// Object attributes can also be accessed using the subscript syntax,
myObj["my other key"]; // = 4

// ... or using the dot syntax, provided the key is a valid identifier.
myObj.myKey; // = "myValue"

// Objects properties are mutable; values can be changed and new keys added.
myObj.myThirdKey = true;

// If you try to access a value that's not yet set, you'll get undefined.
myObj.myFourthKey; // = undefined

## Logic and Control Structures

// The `if` structure works as you'd expect.
const count = 1;
if (count == 3){
    // evaluated if count is 3
} else if (count == 4){
    // evaluated if count is 4
} else {
    // evaluated if it's not either 3 or 4
}

// As does `while`.
while (true){
    // An infinite loop!
}

// Do-while loops are like while loops, except they always run at least once.
let input;
do {
    input = getInput();
} while (!isValid(input));

/**
* The `for` loop is the same as C and Java:
* initialization; continue condition; iteration.
**/
for (let i = 0; i < 5; i++){
    // will run 5 times
}

// Breaking out of loops is similar to Java
for (let i = 0; i < 10; i++) {
  if (i === 3) {
    break;
  }
  text += "The number is " + i + "<br>";
}

// The `continue` statement breaks one iteration of a loop
for (let i = 0; i < 10; i++) {
  if (i === 3) {
    continue;
  }
  text += "The number is " + i + "<br>";
}

/**
* Using break with a label breaks the labeled statement.  
* You can use labelled breaks to jump out of _all_ loops
**/
foo:
for (let i = 0; i < 10; i++) {
    for (let j = 0; j < 10; j++) {
        if (i === 5 && j === 5) {
            break foo;
            // breaks out of outer loop instead of only the inner one
        }
    }
}

// The for/in statement allows iteration over properties of an object.
let description = "";
const person = {fname:"Paul", lname:"Ken", age:18};
for (let x in person){
    description += person[x] + " ";
} // description = 'Paul Ken 18 '

/**
* The for/of statement allows iteration over iterable objects (including the built-in `String`, 
* `Array`, `Map`, `Set`, and user-defined iterables).
**/
let myPets = "";
const pets = ["cat", "dog", "hamster", "hedgehog"];
for (let pet of pets){
    myPets += pet + " ";
} // myPets = 'cat dog hamster hedgehog '

// `&&` is logical and, `||` is logical or
if (house.size == "big" && house.colour == "blue"){
    house.contains = "bear";
}
if (colour == "red" || colour == "blue"){
    // colour is either red or blue
}

/**
* `&&` and `||` use ([lazy evaluation](https://en.wikipedia.org/wiki/Lazy_evaluation#JavaScript)),
* which is useful for setting default values.
**/
let name = otherName || "default";

/**
* The `switch` statement checks for equality with `===`.
* Use `break` after each case or the cases after the correct one will be executed too.
**/
switch (grade) {
  case 'A':
    console.log("Great job");
    break;
  case 'B':
    console.log("OK job");
    break;
  case 'C':
    console.log("You can do better");
    break;
  default:
    console.log("Oy vey");
    break;
}
```

## Functions, Scope and Closures

```js
/**
* JavaScript functions are declared with the `function` keyword.
* Note that the value to be returned must start on the same line as the
* `return` keyword, otherwise you'll always return `undefined` due to
* automatic semicolon insertion.
**/
function myFunction(thing){
    return thing.toUpperCase();
}
myFunction("foo"); // = "FOO"

/**
* However, [ES6](https://www.w3schools.com/js/js_es6.asp) introduced "lambda syntax".
* This allows functions to be defined in a lexical scope exactly like variables.
**/
const isEven = (number) => {
    return number % 2 === 0;
};

/**
* JavaScript functions are first class objects, so they can be reassigned to
* different variable names and passed to other functions as arguments.
* For example, when supplying an event handler:
**/
function myFunction(){
    // this code will be called in 5 seconds' time
}
setTimeout(myFunction, 5000);

/**
* Note: setTimeout isn't part of the language itself,
* instead, it is provided by browsers and [node.js](https://nodejs.org/en/).
**/

// Another function provided by browsers is `setInterval`
function myFunction(){
    // this code will be called every 5 seconds
}
setInterval(myFunction, 5000);

/**
* Function objects don't even have to be declared with a name - you can write
* an anonymous function definition directly into the arguments of another.
**/
setTimeout(function(){
    // this code will be called in 5 seconds' time
}, 5000);

// Or, using arrow function syntax
setTimeout(() => {
    // this code will be called in 5 seconds' time
}, 5000);

/**
* One of JavaScript's most powerful features is closures. If a function is
* defined inside another function, the inner function has access to all the
* outer function's variables, even after the outer function exits.
**/
const sayHelloInFiveSeconds = (name) => {
  const prompt = "Hello, " + name + "!";
  // Inner functions are put in the local scope by default, as if they were
  // declared with `var`.
  function inner() {
    alert(prompt);
  }
  setTimeout(inner, 5000);
  // setTimeout is asynchronous, so the sayHelloInFiveSeconds function will
  // exit immediately, and setTimeout will call inner afterwards. However,
  // because inner is "closed over" sayHelloInFiveSeconds, inner still has
  // access to the `prompt` variable when it is finally called.
};
sayHelloInFiveSeconds("Adam"); // will open a popup with "Hello, Adam!" in 5s
```

## More About Objects

```js
// Objects can contain functions.
const myObj = {
    myFunc: function(){
        return "Hello world!";
    }
};
myObj.myFunc(); // = "Hello world!"

/**
* When functions attached to an object are called, they can access the object
* they're attached to using the `this` keyword.
**/
myObj = {
    myString: "Hello world!",
    myFunc: function(){
        return this.myString;
    }
};
myObj.myFunc(); // = "Hello world!"

// The function doesn't work if it isn't called in the context of the object.
let myFunc = myObj.myFunc;
myFunc(); // = undefined

/**
* A function can be assigned to the object and gain access to that object
* through `this`, even if it wasn't attached when it was defined.
**/
const myOtherFunc = function() {
    return this.myString.toUpperCase();
};
myObj.myOtherFunc = myOtherFunc;
myObj.myOtherFunc(); // = "HELLO WORLD!"

/**
* You can also specify a context for a function to execute in by invoking it
* using `call` or `apply`.
**/
const anotherFunc = function(s) {
    return this.myString + s;
};
anotherFunc.call(myObj, " And Hello Moon!"); // = "Hello World! And Hello Moon!"

// The `apply` function is closely related to `call`, but takes an array for an argument list.
anotherFunc.apply(myObj, [" And Hello Sun!"]); // = "Hello World! And Hello Sun!"

/**
* This is useful when working with a function that accepts a sequence of
* arguments and you want to pass an array.
**/
Math.min(42, 6, 27); // = 6
Math.min([42, 6, 27]); // = NaN (uh-oh!)
Math.min.apply(Math, [42, 6, 27]); // = 6

// But, `call` and `apply` are only temporary. When we want it to stick, we can
// use `bind`.
const boundFunc = anotherFunc.bind(myObj);
boundFunc(" And Hello Saturn!"); // = "Hello World! And Hello Saturn!"

// `bind` can also be used to partially apply a function.
let product = function(a, b){ return a * b; };
let doubler = product.bind(this, 2);
doubler(8); // = 16
```

## Constructors and Prototypes

```js
/**
* Every JavaScript object has a built-in 'prototype' property,
* which is the mechanism by which JavaScript objects inherit features from one another.
**/

* Below, `myObject` is an object with one data property, city, and one method, greet().
* However, if you type the object's name followed by a period into the console (`myObject.`),
* the console will pop up a list of all the properties available to this object.
* You'll see that as well as city and greet, there are lots of other properties
**/
const myObject = {
  city: 'Madrid',
  greet() {
    console.log(`Greetings from ${this.city}`);
  }
}
myObject.greet(); // Greetings from Madrid

/**
* The prototype is itself an object, so the prototype will have its own prototype, 
* making what's called a prototype chain.
* When you go to access a property on an object that doesn't exist on the actual object,
* the interpreter will look at its prototype.
**/

/**
* When you try to access a property of an object: if the property can't be found in the object itself,
* the prototype is searched for the property. If the property still can't be found, then the prototype's * prototype is searched, and so on until either the property is found, or the end of the chain is
* reached, in which case undefined is returned.
**/

/* `Object.create` and constructors are ways of setting an object's prototype in JavaScript

/**
*`Object.create`
* This creates a new object and allows you to specify an object
* that will be used as the new object's prototype.
**/
const personPrototype = {
  greet() {
    console.log('hello!');
  }
}

const carl = Object.create(personPrototype);
carl.greet();  // hello!

/**
* Constructors
* A constructor in JavaScript is just a function that happens to be called with the `new` operator.
**/
function Graph() {
  this.vertices = [];
  this.edges = [];
}

Graph.prototype.addVertex = function(v) {
  this.vertices.push(v);
}

const g = new Graph(); // g is an object with own properties 'vertices' and 'edges'.
g.addVertex('A') // g.vertices = ['A']

// You can extend built-in object (or array) prototypes, too (although, this is frowned upon)
Array.prototype.doubleUp = function () {
  return this.map((element) => {
    return [element, element];
  }).flat();
};

[1, 2].doubleUpAgain(); // [1, 1, 2, 2]
```

## Classes

```js
/**
* Unlike popular object-oriented languages, javaScript does not include 
* the concept of 'instances' created from 'class' blueprints
* However, ES6 introduced the `class` keyword, which are  "special functions" built on object prototypes
* The result is that javascript classes behave very similarly to classes in other languages  
* because they are a template for creating objects that encapsulate data and the
* code to work on that data.
**/

/**
* The `constructor` method is a special method for creating and initialising an object created with a 
* class. There can only be one special method with the name "constructor" in a class.
**/
class Person {
  name;

  constructor(name) {
    this.name = name;
  }

  introduceSelf() {
    console.log(`Hi! I'm ${this.name}`);
  }
}

const thisPerson = new Person('Steve'); //
thisPerson.introduceSelf() // Steve

// Classes must be defined before they can be constructed.
const p = new Rectangle(); // ReferenceError
class Rectangle {}

/**
* JavaScript object prototypes are the mechanism by which JavaScript objects inherit 
* features from one another. Hence, prototypes support a version of inheritance,
* which is a feature of object-oriented programming languages that express the idea that some objects
* are more specialized versions of others. Such specialisations inherit the common properties,
* while adding and redefining those properties which need to differ.
**/
class Student extends Person {

  #year;

  constructor(name, year) {
    super(name);
    this.#year = year;
  }

  introduceSelf() {
    console.log(`Hi! I'm ${this.name}, and I'm in year ${this.#year}.`);
  }

  canStudyMonads() {
    return this.#year > 1;
  }
}
```