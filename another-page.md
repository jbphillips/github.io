---
layout: default
---

## LocalStorage and sessionStorage

LocalStorage is not very popular (due to size browser sizing constraints and lack of consistency), yet it is great (and fairly cross-browser) way for storing lots of data for mobile. About 2.49-4.98MB worth depending on the browser. Check how much your browser can store by using this nifty tool by [Nemikor](http://dev-test.nemikor.com/web-storage/support-test/).

Setting and getting with localStorage is dead simple. Consider this JavaScript example here:

```
localStorage.setItem("test", "Hello World!"); //It's saved!
var test = localStorage.getItem("test"); //Let's grab it and save it to a variable
console.log(test); //Logs "Hello World!"
```

Easy peasy. Except when you try something like this:

```
​var test = { test: "thing", test2: "thing2", test3: [0, 2, 44] }​​​​​​​;
localStorage.setItem("test", test);
var test2 = localStorage.getItem("test");
console.log(test2); //Logs "[object Object]"
```

Okay so, as you may notice (besides my bad variable naming), localStorage doesn’t like objects or even arrays. This is where JSON comes to the rescue. Using the ultra cool JSON.stringify function, we can turn this object into a string – since strings are things localStorage does indeed like. While it’s true that JSON functions aren’t available natively in many older browsers, such as IE7, and Firefox 3.0 – we don’t have to worry about that since we are talking about localStorage, a new HTML5 functionality which requires a new-ish browser anyways. If you still can’t use it for some reason, just take a look at JSON source and copy the function for yourself.

```
​var test = { test: "thing", test2: "thing2", test3: [0, 2, 44] }​​​​​​​;
localStorage.setItem("test", JSON.stringify(test));
var test2 = localStorage.getItem("test");
console.log(test2); //Logs "{"test":"thing","test2":"thing2","test3":[0,2,44]}"
```

Very cool! It worked. How about taking it a step further and loading them back in as variables/objects? Normally we would have to use the super duper evil eval(). Or, we could even use the window[] trick to evaluate strings as variables from the global scope. But why not take advantage of another great JSON function? JSON.parse can do the trick. Yes, it’s true that JSON.parse does in fact use eval(), it makes sure it’s clean first by only allowing JSON data.

```
​var test = { test: "thing", test2: "thing2", test3: [0, 2, 44] }​​​​​​​;
localStorage.setItem("test", JSON.stringify(test));
var test2 = localStorage.getItem("test");
test = JSON.parse(test2); //var test is now re-loaded!
```

JSON’s .parse is pretty safe, and pretty much native JavaScript in any modern browser.



[back](./)
