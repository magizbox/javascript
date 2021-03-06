# Bacic Syntax

## 1. Code Formatting

Indent with 2 spaces

```javascript
// Object initializer.
var inset = {
  top: 10,
  right: 20,
  bottom: 15,
  left: 12
};

// Array initializer.
this.rows_ = [
  '"Slartibartfast" <fjordmaster@magrathea.com>',
  '"Zaphod Beeblebrox" <theprez@universe.gov>',
  '"Ford Prefect" <ford@theguide.com>',
  '"Arthur Dent" <has.no.tea@gmail.com>',
  '"Marvin the Paranoid Android" <marv@googlemail.com>',
  'the.mice@magrathea.com'
];

// Used in a method call.
goog.dom.createDom(goog.dom.TagName.DIV, {
  id: 'foo',
  className: 'some-css-class',
  style: 'display:none'
}, 'Hello, world!');
```

## 2. Naming

```
functionNamesLikeThis
variableNamesLikeThis
ClassNamesLikeThis
EnumNamesLikeThis
methodNamesLikeThis
CONSTANT_VALUES_LIKE_THIS
foo.namespaceNamesLikeThis.bar
filenameslikethis.js.
```

## 3. Comment

Use [JSDoc](http://usejsdoc.org/)

### 3.1 Class Comment

```javascript
/**
 * Class making something fun and easy.
 * @param {string} arg1 An argument that makes this more interesting.
 * @param {Array.<number>} arg2 List of numbers to be processed.
 * @constructor
 * @extends {goog.Disposable}
 */
project.MyClass = function(arg1, arg2) {
  // ...
};
goog.inherits(project.MyClass, goog.Disposable);
```

### 3.2 Method Comment

```javascript
/**
 * Operates on an instance of MyClass and returns something.
 * @param {project.MyClass} obj Instance of MyClass which leads to a long
 *     comment that needs to be wrapped to two lines.
 * @return {boolean} Whether something occurred.
 */
function PR_someMethod(obj) {
  // ...
}
```
## 4. Expression and Statements
####Expression
*A fragment of code that produces a value is called an Expression*
```javascript
22
"this is an epression"
(5 > 6) ? false : true
```
####Statements
The Simplest kind of stagement is an expression with a semi colon
```javascript
!false;
5 + 6;
```
## 5. Loop and iteration
####while
```javacript
  var number = 0;
  while (number <= 12) {
  console.log(number);
  number = number + 2;
}
```
####do..while
```javascript
do {
  var yourName = prompt("Who are you?");
} while (!yourName);
console.log(yourName);
```
####for
```javascript
for (var i = 0; i < 10; i++) {
  console.log(i);
}
```

```javascript
var objects = {a:1, b:2, c:3, d:4, e:5};
for (object in objects) {console.log(object)};
```

## 6. Function
### 6.1 Defining a Function

+ define a function
```javascript
function add(a, b) {
  return a + b;
}
add(1, 2);
```

+ function as variable
```javascript
var square = function(x) {
  return x * x;
};
square(5);
```

+ Anonymous function
```javascript
setTimeout(function(){
  console.log("this is inside a anonymous function. It is usually used as a callback function");
}, 1000);

```
### 6.2 Scope
#####Scope is the area where contains all variable or function are living. </br>
#####Scope has some rules:
+ Child Scope can access all variable and function in parent Scope. (E.g: Local Scope can access Global Scope)
```javascrpit
function saveName(firstName) {
    var temp = "temp";
    function capitalizeName() {
        temp = temp + " here";
        return firstName.toUpperCase();
    }
    var capitalized = capitalizeName();
    return capitalized;
}
alert(saveName("Robert"));
```
+ But parent Scope can access variable and function inside children scope (E.g: Global Scope cannot acces to local Scope)
```javascript
function talkDirty () {
    var saying = "Oh, you little VB lover, you";
    return alert(saying);
}
alert(saying); //->Error
```
### 6.3 Call Stack

The storage where computer stores context is called CALL STACK.

```javascript
// CALL STACK
function greet(who) {
    console.log("Hello " + who);
    ask("How are you?");
    console.log("I'm fine");
};

function ask(question) {
    console.log("well, " + question);
};

greet("Harry");
console.log("Bye");
```

Out of Call Stack
```javascript
function chicken() {
    return egg();
}

function egg() {
    return chicken();
}
console.log(chicken() + " came first");
```

### 6.4. Optional Argument

#### We can pass too many or too few arguments to the function without any SyntaxError.

* If we pass too much arguments, the extra ones are ignored
* If we pass to few arguments, the missing ones get value undefined

```javascript
function power(base, exponent) {
    if (exponent == undefined) {
        exponent = 2;
    }
    var result = 1;
    for (var count = 0; count < exponent; count++) {
        result = result * base;
    }
    return result;
}
console.log(power(4)); 
console.log(power(4,3));
```
**upside**: flexible </br>
**downside**: hard to control the error

### 6.5 Closure

Look at this example:

```javascript
function sayHello(name){
    var text = 'Hello' + name;
    var say = function(){
        console.log(text);
    }
    return say;
}
var say2 = sayHello("ahaha");
say2();
```

if in C program, does say2() work? <br/>
The answer is nope! Because in C program, when a function returns, the Stack-flame will be destroyed, and all the local variable such as *text* will undefinded. So, when say2() is called, there is no text anymore, and the error, will be shown! </br>
But, in JavaScript, This code works!! Because, it provides for us an Object called Closure! Closure is borned when we define a function in another function, it keep all the live local variable. So, when say2() is called, the closure will give all the value of local variable outside it, and text will be identity.!

```javascript
var globalVariable = 10;
function func(){
    var name = "xxx";
    function getName(){
        return name;
    }
    function speak(){
        var sound = "alo";
        function scream(){
            console.log(globalVariable);
            console.log(name);
            return "aaaaaaaaaa!";
        }
        function talk(){
            var voice = getName() + " speak " + sound;
            console.log(voice);
            return voice;
        }
        scream();
        talk();
    }
    speak();
}
func();
```

### 6.6. Recursion
Recursion is  function can call itself, as long as it is not overflow
```javascript
function power(base, exponent){
    if (exponent == 0){
        return 1;
    }
    else{
        return base * power(base, exponent -1);
    } 
}
console.log(power(2,3));

function FindSolution(target){
    function Find(start, history){
        if (start == target){
            return history;
        }
        else if (start > target){
            return null;
        } 
        else{
            return Find(start + 5, "(" + history + " + 5 ") ||
            Find(start * 3, "(" + history + " * 3)");
        }
    }
    return Find(1, "1");
}
console.log(FindSolution(25));   
```
### 6.7. Arguments object
The arguments object contains all parameters you pass to a function.
```javascript
function argumentCounter() {
    console.log("you gave me", arguments.length, "argument.");
}
argumentCounter("Straw man", "Tautology", "Ad hominem");
```

### 6.8. Higher-Order Function
```javasript
###Filter array
var ancestry = JSON.parse(ANCESTRY_FILE);
console.log(ancestry.length);

function filter(array, test) {
    var passed = [];
    for (var i = 0; i < array.length; i++){
        if (test(array[i])){
            passed.push(array[i]);
        }
    }
    return passed;
}
console.log(filter(ancestry, function(person){
    return person.born > 1900 && person.born < 1925;
}));

### TRANSFORMING WITH A MAP
function map(array, transform) {
  var mapped = [];
  for (var i = 0; i < array.length; i++)
    mapped.push(transform(array[i]));
  return mapped;
}

var overNinety = ancestry.filter(function(person) {
  return person.died - person.born > 90;
});
console.log(map(overNinety, function(person) {
  return person.name;
}));


### REDUCE
function reduce(array, combine, start) {
  var current = start;
  for (var i = 0; i < array.length; i++)
    current = combine(current, array[i]);
  return current;
}
console.log(reduce([1, 2, 3, 4], function(a, b) {
  return a + b;
}, 0));
#Problem: using map and reduce, transform [1,2,3,4] to [1,2],[3,4]

var a = [1, 2, 3, 4]
a = _.map(a, function(i){
    if(i % 2 == 0){
        return [[],[i]]
    } else {
        return [[i], []]
    }
});
a = _.reduce(a, function(x, y){
   return [x[0].concat(y[0]), x[1].concat(y[1])]
})


### BINDING FUNCTION
var theSet = ["Carel Haverbeke", "Maria van Brussel",
              "Donald Duck"];
function isInSet(set, person) {
  return set.indexOf(person.name) > -1;
}

console.log(ancestry.filter(function(person) {
  return isInSet(theSet, person);
}));
console.log(ancestry.filter(isInSet.bind(null, theSet)));
```

[^1]: [What's the cleanest way to write a multiline string in JavaScript? [duplicate]](http://stackoverflow.com/questions/1589234/whats-the-cleanest-way-to-write-a-multiline-string-in-javascript)
[^2]: [Google JavaScript Style Guide](https://google.github.io/styleguide/javascriptguide.xml)