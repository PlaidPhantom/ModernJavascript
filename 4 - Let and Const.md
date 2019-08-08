# Let and Const

In Javascript, we've been declaring all our variables so far with `var`:

```javascript
var a = 5;
var b = () => {
    var c = 3;
}
```

Now, we have two additional options.

## Let

`let` works basically like `var` with some minor differences.  `var` variables are
always scoped to the function they're in. `let` variables are scoped to the _block_
they are in:

```javascript
function func() {
    // bonus: before initialization, `var` variables can be referenced and return `undefined`
    // `let` variables will throw a ReferenceError
    if (true) {
        var a = 1;
        let b = 2;
    }

    console.log(a); // 1; a is a `var` variable and still exists
    console.log(b); // error; b is a `let` variable and lost scope outside of the `if` block
}
```

Because of this, `let` variables are useful for temporary variables, as they can be reused in multiple blocks.

## Const

The `const` declaration makes the variable a constant that cannot be reassigned.
attributes on objects _may_ be changed, however:

```javascript
const a = 5;
a = 6; // error
const b = { c: 1 };
b = {}; // error
b.c = 2; // ok

```
