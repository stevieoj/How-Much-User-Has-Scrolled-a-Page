
/* Detecting the number of pixels the user has scrolled

To detect how much the user has scrolled the page vertically in terms of pixels from the very top,
in JavaScript, we would probe either window.pageYOffset, or in older versions of IE,
 one of several variants of document.body.scrollTop, whichever property is supported */


 var scrollTop = window.pageYOffset || (document.documentElement || \
 	document.body.parentNode || document.body).scrollTop

 //Detecting how far the user has scrolled the page percentage wise

 /* To get the total scrollable area of a document, we need to retrieve the following two measurements of the page:

1. The height of the browser window
2. The height of the entire document 
By subtracting 1 from 2, we get the total scrollable area of the document. */

/*  Getting the height of the browser window

To get the height of the browser window in JavaScript, 
use window.innerHeight, and for IE8 or below, a variant of document.body.clientHeight: */

var winheight = window.innerHeight || (document.documentElement || document.body).clientHeight


/* Getting the height of the entire document

For retrieving the height of the entire document in JavaScript, parts of which may be hidden
behind the browser frame, we need to examine multiple properties and select the largest value
out of the bunch. This is due to inconsistencies in some browsers when it comes to interpreting
the height of a document with no vertical scrollbar- what we want in this case is simply the window's height,
though some browsers (ie: Mobile Chrome in Android) will return the height of the content contained
inside the document instead. To get the desired document height across the board, 
we can use James Padolsey's function for that */

function getDocHeight() {
    var D = document;
    return Math.max(
        D.body.scrollHeight, D.documentElement.scrollHeight,
        D.body.offsetHeight, D.documentElement.offsetHeight,
        D.body.clientHeight, D.documentElement.clientHeight
    )
}
 
var docheight = getDocHeight()


/*  Putting it all together

We have all the pieces now for determining how much the user has scrolled in 
terms of percentage. First up is the JavaScript version- we'll attach all our 
code to window's onscroll event to see the output change as the user scrolls  */

function amountscrolled(){
    var winheight= window.innerHeight || (document.documentElement || document.body).clientHeight
    var docheight = getDocHeight()
    var scrollTop = window.pageYOffset || (document.documentElement || document.body.parentNode || document.body).scrollTop
    var trackLength = docheight - winheight
    var pctScrolled = Math.floor(scrollTop/trackLength * 100) // gets percentage scrolled (ie: 80 or NaN if tracklength == 0)
    console.log(pctScrolled + '% scrolled')
}
 
window.addEventListener("scroll", function(){
    amountscrolled()
 }, false)

/* Move your eyes down to the trackLength variable, which gets 
the total available scroll length of the document. The variable
will contain 0 if the page is NOT scrollable. The pctScrolled 
variable then divides the scrollTop variable (amount the use has scrolled) 
with trackLength to derive how much the user has scrolled percentage wise */


/*  Applying some optimizations inside onscroll

Running code inside window's onscroll event can be an expensive affair, as the code is often 
invoked many times per second as the user obliviously scrolls. Looking at our code for getting 
how many percent of the page the user has scrolled above, here's a couple of optimizations we can perform:

Cache the winheight, docheight, and trackLength variables' values, and only refresh them when the page has 
resized, instead of each time the page is scrolled.

Throttle the code inside window onscroll so they are executed only once per a certain period (ie: 300 milliseconds), 
using JavaScript's setTimeout() method.

With that said, here is the JavaScript version of our optimized code to get how much the user has scrolled percent wise
as he/she scrolls */



var winheight, docheight, trackLength, throttlescroll
 
function getmeasurements(){
    winheight= window.innerHeight || (document.documentElement || document.body).clientHeight
    docheight = getDocHeight()
    trackLength = docheight - winheight
}
 
function amountscrolled(){
    var scrollTop = window.pageYOffset || (document.documentElement || document.body.parentNode || document.body).scrollTop
    var pctScrolled = Math.floor(scrollTop/trackLength * 100) // gets percentage scrolled (ie: 80 or NaN if tracklength == 0)
    console.log(pctScrolled + '% scrolled')
}
 
getmeasurements()
 
window.addEventListener("resize", function(){
    getmeasurements()
}, false)
 
window.addEventListener("scroll", function(){
    clearTimeout(throttlescroll)
        throttlescroll = setTimeout(function(){ // throttle code inside scroll to once every 50 milliseconds
        amountscrolled()
    }, 50)
}, false)

/* Conclusion

Detecting how much the user has scrolled forms the basis for many interesting effects, 
such as parallax or opt-in boxes that only pop up when you've reached the bottom of the
page. We now have the essential parts to implement these effects ourselves.  */
