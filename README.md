# JavaScript Looks Familiar

***  

## __Designed to be easy for developers to pick up__  

```javascript
if (encoder.state == "cue record") {
    beginRecording();
}
```

## __Is actually based on the languages Scheme and Self__  

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

## __Provides a root object and an environment API__

* Browser: window object and the DOM + BOM  
* Server: process object and the native modules 

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

***  

# Variables 
### Declared with “var” keyword
### Dynamically typed
### Simple types are copied by value
### Complex types are copied by reference

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









