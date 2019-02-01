--
layout: default
---

#Including the ChromeDriver location in MacOS System PATH

The ChromeDriver getting started guide wasn’t super helpful with it’s installation instructions, mainly because I was unfamiliar with including the ChromeDriver location in my PATH environment variable (you have to help Chrome find the downloaded ChromeDriver). Don’t get me wrong, I’ve updated PATH variables on Windows for years but never on a Mac, until now:

System PATH Setup
The following instructions will help you create your own PATH to a unique folder on your Mac or copy the file to an existing PATH directory for ChromeDriver.

*Download the ChromeDriver executable.
*Now we need to tell Selenium where it is and for that we have a few choices.To do this:
*Open up Terminal
*Run sudo nano /etc/paths
*Enter your password
*Go to the bottom of the file and enter the path you wish to add
*My PATH looks like: /Users/name/Documents/WebDriver
*Control-x to quit
*Y to save
*Press enter to confirm

To double check, quit Terminal and relaunch it. Run echo $PATH. You should see your newly added path in the stream of other paths already there.

Finally, update your tests to run using Chrome and run your tests!

After running your tests, if your PATH isn’t set up correctly you get this helpful message:

Selenium::WebDriver::Error::WebDriverError: Unable to find the chromedriver executable. Please download the server from http://chromedriver.storage.googleapis.com/index.html and place it somewhere on your PATH. More info at http://code.google.com/p/selenium/wiki/ChromeDriver.

Additional References:

Adding to the PATH on a Mac
Installing ChromeDriver on macOS
Related