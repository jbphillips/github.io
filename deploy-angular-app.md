---
layout: default
---

## Deploy an Angular App

ng build --prod --base-href /zircon/

The Angular CLI allows you to run a command that creates a build for production, which we will be using. Lets go!

## Creating a Production Build

Angular CLI has the ability to create a production build of your app, along with AOT (Ahead of Time) compilation.

In the end, the ultimate goal is to create an app that is as small as possible in file size. So, to demonstrate this, let's run the following command in the console within an Angular project setup to work with the CLI:

    >ng build

When you run the ng build command, it creates a /dist folder. Here are the files and their associated sizes after running the above command.

Note: Your file sizes will vary based on your project.

    vendor.bundle.js              2.2 MB
    polyfills.bundle.js           163 KB
    main.bundle.js                13  KB
    inline.bundle.js              6   KB
    styles.bundle.js              10  KB

As you can see, we have a massive vendor.bundle.js file, because when you run ng build without specifying the production environment, it doesn't make use of uglifying and tree-shaking.

Let's re-run the ng build command, but specify the --prod flag (for production):

    > ng build --prod

Now let's look at the sizes:

    vendor.bundle.js              352 KB    // Reduced from 2.2 MB
    polyfills.bundle.js           57  KB    // Reduced from 163 KB
    main.bundle.js                12  KB    // Reduced from 13  KB
    inline.bundle.js              2   KB    // Reduced from 6   KB
    styles.bundle.js              0   KB    // Reduced from 10  KB

So, adding the production flag reduced the bundle from around 2.4 MB to 423 KB, which is nearly an 83% reduction.

How does it do this? Well, a number of things are occurring when you add the --prod flag:

Removes unwanted white space by minifying files.
Uglifies files by renaming functions and variable names.
AoT compilation, which removes the compilation process at runtime and instead performs compilation during the build process.
All of these things drastically reduce the file size of your Angular app, thus decreases load times.

Something important: You may have heard of AoT (Ahead of Time Compilation). As of March 1, 2017, when you specify the --prod flag as we did above, it automatically includes AoT. Previously, you had to explicitly specify an --aot flag.

## Deploying your build

Now that your app is ready to go in the /dist folder, what do we do to show it to the world?  Well, you have several options.

If your app does not contain a backend, you can simply take the contents of the /dist folder and upload them to your site. The app will work if you're uploading it to the root public folder, such as mysite.com, but if it's within a sub folder such as mysite.com/whatever, you can specify the --base-href flag during the build process based on the folder structure of where the app will be placed.

Outside of uploading the files via FTP, you can quickly deploy your app to GitHub Pages using angular-cli-ghpages. 

The ability to deploy to GH Pages was previously a part of the Angular CLI, but it has been recently removed. It's now in its own package, so let's install that.

    > npm i -g angular-cli-ghpages

Next, login to your github.com account and create a new repository for your Angular project.

Also, run through the steps it suggests to turn your project directory into a git repository (Note: You will need the git client)

    > git init
    > git add .
    > git commit -m "First commit"
    > git remote add origin remote-repository-url
    > git push origin master

You're only able to use the angular-cli-ghpages CLI if you have a /dist folder. If you do, you can then run:

    > ngh

With any luck, you can visit your Github Page URL for that project and it will now load your Angular app.

Should you run into any issues with the app not loading, it's likely because you did not use, or did not use correctly, the ng build --prod --base-href "https://USERNAME.github.io/REPOSITORY/" command. 


[back](./)
