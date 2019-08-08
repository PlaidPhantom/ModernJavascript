# Async and Await

Promises are all nice and good on their own, but their real benefit comes with the
addition of the `async` and `await` keywords.  In concept, they are similar to C#'s
async/await functionality, except they are built on Promises instead of Tasks. The
Javascript engine compiles async functions to promise chains internally.

This Promise-based code:

```javascript
function promiseFunction() {
    return fetch('/somedata')
    .then(response => response.json())
    .then(data => { return data.interestingPart; })
    .catch(error => {
        console.log(error);
    });
}
```

is equivalent to:

```javascript
// async functions always return a promise
async function asyncFunction() {
    try {
        // await can *only* be used in an async function
        let response = await fetch('/somedata');
        let json = await response.json();
        return data.interestingPart;
    }
    catch (error) {
        console.log(error);
    }
}

```

Promises and `async`/`await` can be mixed freely:

```javascript
function sleep(msecs) {
    return new Promise((resolve, reject) => {
        setTimeout(resolve, msecs);
    });
}

let sleepSeconds = async seconds => await sleep(seconds * 1000); // arrow functions can be async too!

sleepSeconds(5).then(() => {
    console.log('five seconds later!');
})

```
