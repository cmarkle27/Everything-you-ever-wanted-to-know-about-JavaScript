# JavaScript Only Looks Familiar

***  

### __Designed to be easy for developers to pick up__  

```javascript
if (encoder.state == "cue record") {
    beginRecording();
}
```

### __Is actually based on the languages Scheme and Self__  

```javascript
function Y(le) {
    return (function (f) {
        return f(f);
    }(function (f) {
        return le(function (x) {
            return f(f)(x);
        });
    }));
}

var sliced = Array.prototype.slice.call(arguments, 2);
```
<br><br><br>

# JavaScript Requires an Environment  

***  

### __Provides a root object and an environment API__

* Browser: window object and the DOM + BOM  
* Server: process object and the native modules 

<br><br><br>
<br><br><br>
<br><br><br>

# Single Threaded and Event Driven 

***  

### Basic flow of execution: 
1. Script is parsed and lexed 
1. Code is executed 
1. Events are registered 
1. Idles in event loop 
1. Triggered events are added to the queue (return to 1) 

```javascript
// one thing at a time
for (var i = 1; i < 1000; i++) {
    console.log(i);
    if (i === 250) alert("Wait!");
}

// events fire asynchronously
var no;

for (var i = 1; i <= 10; i++) {
    no = i;
    setTimeout(function() {
       console.log('setting: ' + no);
    }, 500);
}
```

<br><br><br>

# Variables 

***  

* Declared with “var” keyword
* Dynamically typed
* Simple types are copied by value
* Complex types are copied by reference

```javascript
// simple values like are copied by value
var a = 7;
var b = a;
a = 4;
console.log(a, b);

// complex values are passed by reference
var yourCar = new Object();
yourCar.make = "Ford";
yourCar.model = "Mustang";
yourCar.mileage = 28000;

var myCar = yourCar;
yourCar.mileage = 30000;

console.log(myCar);
```

<br><br><br>

# Everything is an Object 

***  

### Even primitives are objects

```javascript
// strings are objects
var name = "Christopher";
console.log(typeof name, name.length);

// numbers are objects
var myNumber = 13.27;
console.log(typeof myNumber, myNumber.toFixed());

// objects are objects
var obj = {
  "title": "Leviathan Wakes",
  "author": "James S. A. Corey"
  "pages": 561
}
console.log(typeof obj, obj.author)

// functions are objects
var fun = function myFun() {}
console.log(typeof fun, fun.name);
```

### Objects can contain simple or complex types

```javascript
var recording = new Object();

// number
recording.duration = 31000;

// string
recording.slug = "Cat Roomba Video";

// array
recording.tags = ["funny", "lolcat", "roomba"];

// object
recording.meta = {
  "bureau" : "DC",
  "date" : "08/12/2007"
};

// function
recording.getDuration = function() {
  return Math.floor(this.duration / 1000).toFixed();
};

console.log(recording);
```
<br><br><br>

# As Promised

***  

[http://youtu.be/wBqzjH91WFo](http://youtu.be/wBqzjH91WFo)

<br><br><br>
<br><br><br>

# JavaScript is Functional

***  

### Functions can be passed as values

```javascript
var sayHello = function() {
  return "Howdy!";
};

console.log(sayHello())

console.log(sayHello)
```

### This fits well with event driven programming

[http://jsbin.com/zidad/2/edit?html,js,output](http://jsbin.com/zidad/2/edit?html,js,output)

<br><br><br>

# Constructor Functions

***  

### Returns an object instance when used with the new keyword

```javascript
var Animal = function(species) {
  this.species = species;
  this.birthday = "02/11/2014";
  return this; // implied
};

var carl = new Animal("tiger");
console.log(carl);
```

### Nine native object constructor functions

```javascript
// these cause trouble
new String("hello");
new Number(9);
new Boolean(false);

// these are better as literals
new RegExp('\ bt[ a-z] +\ b');
new Object();
new Array("a", "b", "c");
new Function(" x", "y", "return x * y");

// these are ok
new Error("message");
new Date();

// this object is not a constructor
Math
```

<br><br><br>

# JavaScript is Prototypal

***  

### Instances are created from objects instead of classes

```javascript
var Animal = function(species) {
  this.species = species;
  this.birthday = "02/11/2014";
  return this; // implied
};

var carl = new Animal("tiger");

console.log(carl);
console.log(carl.constructor);
console.log(carl instanceof Animal);
console.log(carl instanceof Object);
```


### Inherit built-in properties

```javascript
// inherited object properties
var serenity = { "class": "Firefly", "captain": "Malcolm Reynolds" };

console.log(serenity.toString());
console.log(serenity.constructor);

// inherited function properties
var spaceShip = function launcher(vehicle) {
  console.log(vehicle + " blasting off!");
};

console.log(spaceShip.name);
console.log(spaceShip.length);
console.log(spaceShip.prototype);

// inherited array properties
var groceries = ["turkey", "bread", "cheese", "carrots"];

console.log(groceries.length);
console.log(groceries.reverse());
```

### Can model classical inheritance (but don’t)

```javascript
// Animal Constructor
function Animal(species) { 
	this.species = species;
	this.energy = 15;
	this.sound = "...";
}

// Animal.prototype is a generic object we can add properties to
Animal.prototype.makeNoise = function(){ 
	this.energy -= 3;
	console.log(this.sound);
};

Animal.prototype.reportEnergy = function(){ 
	console.log("Energy Level:", this.energy);
}; 

Animal.prototype.eat = function(food){ 
	if (food instanceof Food) {
		this.energy += 5;
	}
};  

Animal.prototype.sleep = function(){ 
    this.energy += 10;
};

// Tiger Constructor
var Tiger = function() { 
    this.sound = 'Meow!';
};

Tiger.prototype = new Animal('Tiger');
 
Tiger.prototype.eat = function(food){ 
    if (food instanceof Food && food.type !== 'grain') {
	this.energy += 5;
    }
};

// Instance
var timmy = new Tiger();

console.log(timmy);
```
### Duck Typing

```javascript
var Animal = {
    makeNoise: function() {
	this.energy -= 3;
    	console.log(this.sound + " I am a " + this.species + ". Energy: " + this.energy);
    }
};

// Tiger Constructor
var Tiger = function() { 
    this.sound = 'Meow!';
    this.species = 'Tiger';
    this.energy = 15;  
};

var timmy = new Tiger();

// use duck typing
Animal.makeNoise.call(timmy);
```

<br><br><br>

# The Scope Chain

***  

### Function level (not block level)

```javascript
var foo = 0; // global scope 
console.log(foo); // logs 0

var myFunction = (function() {
    var foo = 1; // local scope
    console.log(foo); // logs 1
	
    var myNestedFunction = (function() {
        var foo = 2; // local scope
        console.log( foo); // logs 2
    })();

})();

eval('var foo = 3; console.log( foo);'); // eval() scope

```

### Variables are defined at parse time (lexical scoping)

```javascript
var x = 10;
var foo = function() {
    var y = 20;
    var bar = (function() {
        var z = 30;
        console.log(z + y + x); // z is local, y & z are found in the scope chain
    })();
};

foo(); // logs 60
```

### Closures 

```javascript
var counterFactory = function() {
    var counter = 0;
    return function() { 
        counter++;
    	console.log(counter);
    }
}

var count = counterFactory();

count();
count();
count();
```

<br><br><br>

# Execution Context

***  

The 'this' Keyword refers to current execution contexts

### Function 

```javascript
function add(x, y) {
    // 'this' refers to the global object 
    var sum = this.x + this.y;

    // most likely NaN
    return sum;
}
```

### Object Method

```javascript
var person = {
    name: "Chris",
    sayHello: function() {
        // refers to the person object
        return this.name; 
    }
}

person.sayHello();
```

### Constructor 

```javascript
function SpaceShip(name) {
    this.name = name; // it depends
    return this; // implied
}

// refers to the new object, this.name will equal "Millennium Falcon"
var transport = new SpaceShip("Millennium Falcon"); 

// refers to the global object, this.name will be undefined
var transport = SpaceShip("Millennium Falcon"); 
```

### Call & Apply

```javascript
var person = {
    name: "Chris",
    sayHello: function() {
        // refers to the invoking object
        return this.name; 
    }
}

var zombie = {
    name: "Fred"
}

// refers to zombie, this.name will be "Fred"
person.sayHello.apply(zombie, params);
```

<br><br><br>

# Resources

***  
* [JavaScript Garden](http://bonsaiden.github.io/JavaScript-Garden/)
* [JavaScript Enlightment](http://www.javascriptenlightenment.com/)
* [JavaScript: Understanding 'this'](https://coderwall.com/p/thslzw)







