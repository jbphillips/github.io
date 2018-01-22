---
layout: default
---

## LocalStorage and sessionStorage

The LocalStorage API gives us access to a simple key-value datastore that can be used to save data on a users computer. Saving data on the client-side can help to speed up the performance of your web applications as it can reduce the number of database queries that are needed on the server. This frees up valuable server resources and can potentially even lead to reduced infrastructure costs.

Before the introduction of LocalStorage, developers that wanted to store data on the client would need to use browser cookies. While this approach did work it had some problems. The first issue is that a cookie can only store 4,096 bytes of data, which isn’t really all that much. Another issue is that cookies are sent up to the server with every HTTP request that is made by the client. This increases the size of requests, leading to higher bandwidth usage and slower request times.

In this blog post you are going to learn how to take advantage of the new LocalStorage API when building your own web applications. Lets go!

## Checking for Browser Support

LocalStorage is a new technology and therefore it is important that we test for browser support and consider fallbacks for browsers that do not support the API. Testing for LocalStorage support is very straight forward. All you need to do is create a simple if statement that contains the localStorage interface as the condition. Note the lowercase ‘l’ in localStorage.

The JavaScript code below shows how you could test to see if a browser supports the LocalStorage API.

    if (localStorage) {
        // LocalStorage is supported!
        } else {
        // No support. Use a fallback such as browser cookies or store on the server.
    }

If the browser does not support LocalStorage you could fallback to using browser cookies or just send the data to be stored on the server.

Now that you understand how to check for support for LocalStorage lets take a look at what the API has to offer.

## Storing Data in LocalStorage

To store data you use the setItem() function. This function takes two parameters, the item key and a value.

    localStorage.setItem('name', 'James Phillips');

Note: There are multiple ways to interact with the localStorage interface. In this blog post I use the functions outlined in the official specification, but you can also treat the localStorage interface like a JavaScript object or array. The examples below will all store data.

    // Functions
    localStorage.setItem('name', 'James Phillips');

    // Object
    localStorage.name = 'James Phillips';

    // Array
    localStorage['name'] = 'James Phillips';

For the remainder of this blog post I will be using functions to interact with the localStorage interface.

Lets take a look at a simple use of LocalStorage in a website. The code below is markup for a contact form. When the user submits the form we are going to save their name so that we can use it later to show them a personalised message.

    <form id="contactForm" action="contact.php" method="POST">
        <div class="field">
            <label for="name">Name</label>
            <input type="text" name="name" id="name">
        </div>
        <div class="field">
            <label for="email">Email</label>
            <input type="email" name="email" id="email">
        </div>
        <div class="field">
            <label for="message">Message</label>
            <textarea name="message" id="message"></textarea>
        </div>
        <div class="field">
            <input type="submit" value="send">
        </div>
    </form>

The JavaScript code below shows how you could intercept the form submission and save the user’s name.

    window.onload = function() {

        // Check for LocalStorage support.
        if (localStorage) {

            // Add an event listener for form submissions
            document.getElementById('contactForm').addEventListener('submit', function() {
            // Get the value of the name field.
            var name = document.getElementById('name').value;

            // Save the name in localStorage.
            localStorage.setItem('name', name);
            });

        }
    }

Now that you know how to save data to the datastore lets take a look at how to get it back out again.

## Retrieving Data from LocalStorage

To retrieve data you use the getItem() function. This takes a single parameter; the key that you used when storing data.

    var name = localStorage.getItem('name');

Building on our previous contact form example, in the code below we retrieve the user’s name from the datastore and then update an element on the page with the text Hello {name}!.

    window.onload = function() {
        ...

        // Retrieve the users name.
        var name = localStorage.getItem('name');

        if (name != "undefined" || name != "null") {
            document.getElementById('welcomeMessage').innerHTML = "Hello " + name + "!";
        } else
            document.getElementById('welcomeMessage').innerHTML = "Hello!";
        }
    }

The if statement is used to make sure that there is a name stored in the database. If we didn’t do this our program might say Hello undefined!. If you attempt to access data that does not exist the localStorage interface will return either null or undefined depending on how you tried to access the data (see the note earlier in this post).

## Removing Data from LocalStorage

To remove an item from the datastore you use the removeItem() function. This function takes the key of the item that you wish to delete.

    localStorage.removeItem('name');

##Clearing the Datastore

If you want to delete all of the data in the datastore you can use the clear() function.

    localStorage.clear();

## Retrieving Keys

The localStorage interface also includes a function calles key(), that can be used to retrieve the key of a data item using the index (numerical position) of the item in the datastore. Admittedly you will probably not be using this function very often but it is useful to know that it exists.

The JavaScript code below shows how you might use this function to output the keys for each of the items in the datastore.

    for (var i = 0; i < localStorage.length; i++) {
    console.log(localStorage.key(i))
    };

Note the use of localStorage.length in this example. The length property tells you how many items are in the datastore.

## Sandboxing and Storage Limits

The data that you add to the LocalStorage datastore is sandboxed to your websites domain name. This means that your web application cannot see the data stored by any other applications and those applications cannot see the data stored by yours. This is an important security measure.

Sub-domains (i.e. a.example.com, b.example.com, c.example.com) are treated as separate domains and are therefore given their own datastore.

There is a limit on how much data you can put in LocalStorage. This limit is set by browser vendors and therefore varies between browsers. To be safe, you should assume that your web application has only 2.5mb of storage space. This should be more than enough space as LocalStorage is only designed to hold basic key-value data. If you find yourself needing more space you might want to reconsider whether LocalStorage is the best storage technology for your application.

## SessionStorage

Data stored in LocalStorage is persitent. This means that if you store some data, close your browser and then open up your appllication again, all of the data will still be retrievable. However you may only want to store some data for the duration of a user session. In this case you can use the sessionStorage interface. This has all of the same functions that localStorage does but the data you save will automatically be wiped when the user closes the browser tab.

    // Storing Data
    sessionStorage.setItem('name', 'Matt West');

    // Retrieving Data
    var name = sessionStorage.getItem('name');

    // Deleting Data
    sessionStorage.removeItem('name');

    // Retrieving an Item Key
    sessionStorage.key(n);

    // Clearing the Datastore
    sessionStorage.clear();

## Thoughts on LocalStorage

The LocalStorage API allows developers to make considerable advances in the performance of their web applications. Looking past this initial advantage, LocalStorage also provides a datastore for offline applications (assuming that a technology like AppCache is being used to make the other application resources available). I am especially interested about the potential applications that LocalStorage has for HTML5 mobile applications. Mobile devices are much more likely to be without an internet connection and therefore without access to traditional server-based datastores.

Useful Links
WebStorage Specification
Can I Use LocalStorage
Client-Side Storage (HTML5 Rocks)



[back](./)
