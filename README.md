# JavaScript Looks Familiar


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
<br><br>

***    
<br><br>

# JavaScript Requires an Environment  

## __Provides a root object and an environment API__

* Browser: window object and the DOM + BOM  
* Server: process object and the native modules 

<br><br>

***    
<br><br>

# Single Threaded and Event Driven 





