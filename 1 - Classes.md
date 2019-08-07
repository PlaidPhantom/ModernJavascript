# Classes

Javascript did not previously have real "OOP" classes; instead we had "prototype" inheritance.

* Everything is just an object
* objects can point to other objects as their "prototype"

```javascript

var alice = {
    name: 'Alice',
    getName: function() {
        return this.name;
    }
};

var bob = {};

Object.setPrototypeof(bob, alice); // or bob.__proto__ = alice; (non-standard)

console.log(bob.name); // 'Alice'
console.log(bob.getName()); // 'Alice'
bob.name = 'Bob';

console.log(bob.name); // 'Bob'
console.log(bob.getName()); // 'Bob'

console.log(alice.name); // 'Alice'

```

Thankfully, functions have a `prototype` property, defining the prototype to use if we
create an object by calling the function using `new`.  This gives us something closer to
a traditional class:

```javascript

function Person(n) {
    this.name = n;
}

Person.prototype.getName = function() {
    return this.name;
}

var c = new Person('Charlie');

console.log(c.getName()); // "Charlie"

```

This is still kind of an ugly syntax, so now we _actually_ get a class syntax:

```javascript

class Person {
    constructor (name) {
        this.name = name;
    }

    getName() {
        return this.name;
    }
}

```
