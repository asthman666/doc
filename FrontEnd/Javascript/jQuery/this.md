## this or $(this)

`$()` is the jQuery constructor function.

`this` is a reference to the DOM element of invocation.

So basically, in `$(this)`, you are just passing the `this` in `$()` as a parameter so that you could call jQuery methods and functions.


If you want jQuery's help to do DOM things just keep this in mind.

    $(this)[0] === this


Basically every time you get a set of elements back jQuery turns it into a jQuery object. If you know you only have one result, it's going to be in the first element.

    $("#myDiv")[0] === document.getElementById("myDiv");
