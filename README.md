### STEP 1 
...shows a basic function call without promises. We simply take two numbers, add them together, and send the result to an alert() box.

### STEP 2 
...does the same thing as STEP 1, except it uses Promises to ensure that a result is returned before it's passed to the alert() box.


If you have your own web server, download and use the <a href="https://github.com/JimBarry/promises-how-to/blob/master/index.html"> index.html from this repo.</a><p> 
If you do not have your own web server, then you can use this: <a href="https://codepen.io/JimBarry/pen/jJgNBd"> Codepen.io sample here</a><p>
Either way, now follow along...

# STEP 1: A SIMPLE VANILLA FUNCTION CALL

## First do this:

Run the index.html as-is (leaving the Promises stuff commented out). What's left is the simplest possible function call I could think of. 

## Then let's walk through this:
 
Lines 5 and 6: Let's set up some values we're going to add together, a=1 and b=2.<br>
Line 35: Here's an HTML button, that when clicked, calls the addThem() function.<br>
Line 17: When the user clicks the button, this addThem() function runs.<br>
Line 20: The values a and b are handed off to the addTwoNumbers() function.<br>
Line 9: The value a is referenced inside the addTwoNumbers() function as the parameter numFirst.<br>
Line 9: The value b is referenced inside the addTwoNumbers() function as the parameter numSecond.<br>
Line 11: The two input values are added together, and a 3 is put into the variable twoNumbersAdded.<br>
Line 13: The value 3 is returned back to Line 20.<br>
Line 20: The result of the addTwoNumbers() function (3) is passed into the variable numsAdded.<br>
Line 25: The contents of the numsAdded variable (in our case: 3) is displayed in an alert() box.<br>
DONE<br>
 
In short, Line 25 needs the numsAdded value that is returned by Line 20. In the example code above, the only reason Line 25 doesn't fail, is NOT because it waited for Line 20 to finish. Rather, the only reason Line 25 works is due to the fact that what's going on inside the addTwoNumbers() function happens so fast, that by the time Line 25 gets around to running, the function called in Line 20 happens to already be done, and the numsAdded value that Line 25 needs is ready. 
 
Some functions in JavaScript take a bit of time to do. We're coding for the web after all. Your function might be making a REST call to a remote web server to retrieve, process, or analyze some data before it can return. In our case above, we're just taking two numbers and adding them. It's all happening client-side and happens faster than you can imagine.
 
But that there can be the problem. Meaning, what if the addTwoNumbers()function had some processing in there that made it take a few seconds to finish? How do we make Line 25 wait for Line 20 to be done?
 
Promises, that's how. Ok, so here we go...

 
# STEP 2 - THE SAME FUNCTION CALL WITH PROMISES
 
## First do this:

Go into the index.html file and uncomment the lines: 19 21 22 24 25 27 
 
## Then let's walk through this:
 
Line 19: We create myPromiseObject and wrap it around Line 20. I've left Line 20 exactly where it is, but added Lines 19, 21, and 22. Rather than calling the addTwoNumbers() function when we get to Line 20, we simply make the addTwoNumbers() function PART OF the configuration of the new Promise object. We don't call the addTwoNumbers() function just yet.<br>
 
Line 24: Rather than calling the addTwoNumbers() function directly, we instead call myPromiseObject with the .then() method. The .then() method is the magic part—it will wait for the function inside myPromiseObject to finish.<br>
 
Lines 19 and 22: Inside these two curly braces go the lines of code that will run when myPromiseObject is done ready (ie, when the code inside myPromiseObject is done running). We're getting there.<br>
 
Line 21: When myPromiseObject resolves (ie, gets a value back from) the addTwoNumbers() function that it calls, the value in the numsAdded variable goes back to the place myPromiseObject was called from. This will become the "result" that you see on Line 24.<br>
 
Line 24: When the addTwoNumbers() function inside myPromiseObject finishes, the "result" parameter contains whatever was passed to the resolve() on Line 21.  In other words, the numsAdded variable from Line 21 becomes the result parameter on Line 24.<br>
 
Line 25: Now that the .then() magic is triggered, the code inside the .then() method’s curly braces runs. In our case above, the value in the "result" parameter is displayed in an alert() box. <br>
