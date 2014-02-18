# JavaScript Looks Familiar


## Designed to be easy for developers to pick up  

```javascript
if (encoder.state == "cue record") {
    beginRecording();
}
```

## Is actually based on the languages Scheme and Self  

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
  
  
  
  
  
  
  
# JavaScript Requires an Environment  

## Provides a root object and an environment API

Browser: window object and the DOM + BOM 

Server: process object and the native modules  




