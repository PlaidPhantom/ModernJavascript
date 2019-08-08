# Arrow functions

In Javascript, `this` is a little weird: it depends on the call site:

```javascript
function makeVal(name, callback) {
    setTimeout(function() { callback(name.length); }, 100);
}

class A {
    constructor(n) { this.name = n; this.val = 0; }
    getNewVal() {
        makeVal(this.name, function(returnedVal) { this.val = returnedVal; });
    }
}

var a = new A('asdf');

a.getNewVal(); // TypeError, `this` is undefined in the anonymous function when called in `makeVal`
```

If we wanted to keep a reference to `a` in this case, we have to jump through some hoops,
or use some of the tools given us:

```javascript
function makeVal(name, callback) {
    setTimeout(function() { callback(name.length); }, 100);
}

class A {
    constructor(n) { this.name = n; this.val = 0; }
    getNewVal() {
        makeVal(this.name, (function(returnedVal) { this.val = returnedVal; }).bind(this)); // ew
    }
    // getNewVal() {
    //     var that = this; // blughghghgh
    //     makeVal(this.name, function(returnedVal) { that.val = returnedVal; });
    // }
}

var a = new A('asdf');

a.getNewVal();
```

To solve this problem, and also give us a nice "lambda"-style function syntax, we get arrow functions.
Arrow functions define `this` _lexically_, meaning whatever `this` is at the point in the code they are defined:

```javascript
function makeVal(name, callback) {
    setTimeout(function() { callback(name.length); }, 100);
}

class A {
    constructor(n) { this.name = n; this.val = 0; }
    getNewVal() {
        makeVal(returnedVal => { this.val = returnedVal; }); // much better!
    }
}

var a = new A('asdf');

a.getNewVal();
```

Arrow functions use less syntax, so they can make blocks with smaller functions much easier to read.

* parentheses around parameter list are not required if there's only one item
* if the braces are dropped, then the body is an expression whose result is the return value of a function.

e.g. `a => a + 1` is equivalent to `function(a) { return a + 1; }`

```javascript
var a = [ 1, 2, 3, 4, 5];

a.filter(item => item > 2).some(item => item % 4 === 0) // filter the list to values greater than two and see if any are divisible by 4
```
