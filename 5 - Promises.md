# Promises

Program flow in Javascript is largely _asynchronous_.  Code is triggered by actions and events
triggered by the user and the environment.  Writing Javascript almost always involves setting
up code to be run later when some event happens:

```javascript
document.querySelector('.mybutton').addEventListener('click', function() {
    alert('button clicked');
});

setTimeout(() => { console.log('done waiting'); }, 500);
```

Callback functions are extremely common in JS, but following the control flow can be confusing,
and APIs can vary.

```javascript
console.log('A');
setInterval(function() {
    console.log('B');
    $.ajax({
        url: '/getdata',
        success: (data, status, jqxhr) => {
            console.log('C');
        },
        error: (jqxhr, status, error) => {
            console.log('D');
        },
        beforeSend: (jqxhr, settings) => {
            console.log('E');
        }
    });

    console.log('F');
}, 5000);

console.log('G');
```

To make things a little easier (and enable some cool stuff in the next lesson),
Promises were introduced to attempt to standardize things:

```javascript
function doAsyncWithPromise() {
    return new Promise((resolve, reject) => {
        someAsyncThing({
            onSuccess: function(returnVal) { resolve(returnVal); },
            onFailure: function(error) { reject(error) }
        });
    });
}

doAsyncWithPromise().then(returnVal => {
    // do something on success
}).catch(error => {
    // handle error
});
```

The nice thing about Promises is that the functions are chainable, and the flow
of the logic is somewhat easier to follow:

```javascript
// new Fetch API
fetch('/somedata')                 // make api call
.then(response => response.json()) // receive response as json
.then(data => {})                  // do something with data
.catch(error => {
    // handle error
});
