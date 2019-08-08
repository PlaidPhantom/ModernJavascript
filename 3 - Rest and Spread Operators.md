# Rest Parameters and Spread Operators

## Rest parameters

Functions can take any number of parameters, but working with them can be a little awkward,
and mixing with named parameters requires special care:

```javascript
function isAnyGreaterThanFirst(compare) {
    // arguments is not actually an array!
    return Array.from(arguments).slice(1, arguments.length).some(a => a > compare);
}

isAnyGreaterThanFirst(5, 1, 4, 9, 4, 3);
```

To make things a little easier, Rest Parameters were added to accept the, well, "rest" of the arguments.

```javascript
function isAnyGreaterThanFirst(compare, ...testCases) {
    var first = arguments[0];
    return testCases.some(a => a > first);
}

isAnyGreaterThanFirst(5, 1, 4, 9, 4, 3);
```

## Spread Operators

On the other side, sometimes we have an array, but a function we're calling wants arguments.
The `Function.apply` method can help:

```javascript
var targetList = [1,2,3,4], myList = [5,6,7,8];
Array.prototype.push.apply(targetList, myList);
```

However we can use the Spread Operator to make this a little easier:

```javascript
var targetList = [1,2,3,4], myList = [5,6,7,8];
targetList.push(...myList);
```

We can even mix regular arguments in:

```javascript
var targetList = [1,2,3,4], myList = [5,6,7,8];
targetList.push(...myList, 9, 10);
```

Even easier, we can use it directly in another array:

```javascript
var targetList = [1,2,3,4], myList = [5,6,7,8];
targetList = [...targetList, ...myList, 9, 10 ];
```
