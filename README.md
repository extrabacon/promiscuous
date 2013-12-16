# promiscuous
<a href="http://promises-aplus.github.com/promises-spec">
  <img src="http://promises-aplus.github.com/promises-spec/assets/logo-small.png"
       alt="Promises/A+ logo" title="Promises/A+ 1.0 compliant" align="right" />
</a>

promiscuous is the smallest implementation of the [Promises/A+ spec](http://promises-aplus.github.com/promises-spec/).

It is promise/deferred library in JavaScript, **small** (< 1kb [minified](https://raw.github.com/RubenVerborgh/promiscuous/dist/promiscuous-node.js) / < 0.6kb gzipped) and **fast**.

## Installation and usage
### Node
First, install promiscuous with npm.
```bash
$ npm install promiscuous
```

Then, include promiscuous in your code file.
```javascript
var promiscuous = require('promiscuous');
```

### Browsers
Include [promiscuous](https://raw.github.com/RubenVerborgh/promiscuous/dist/promiscuous-browser.js) in your HTML file.
```html
<script src="promicuous-browser.js"></script>
```

This version (and a minified one) can be build with:
```bash
$ build/build.js
```

## API
### Create a resolved promise
```javascript
var one = promiscuous.resolve("one");
one.then(console.log);
/* one */
```

### Create a rejected promise
```javascript
var none = promiscuous.reject("error");
none.then(console.log, console.error);
/* error */
```

### Write a function that returns a promise
```javascript
function promiseSomething(something) {
  var defer = promiscuous.deferred();
  setTimeout(function () {
    if (something)
      defer.resolve(something);
    else
      defer.reject("nothing");
  }, 1000);
  return defer.promise;
}
promiseSomething("something").then(console.log, console.error);
/* something */
```