`async`

**For classic scripts, if the async attribute is present, then the classic script will be fetched in parallel to parsing and evaluated as soon as it is available.**

**This attribute allows the elimination of parser-blocking JavaScript where the browser would have to load and evaluate scripts before continuing to parse. defer has a similar effect in this case.**

`defer`

**This Boolean attribute is set to indicate to a browser that the script is meant to be executed after the document has been parsed, but before firing DOMContentLoaded.**

**Scripts with the defer attribute will prevent the DOMContentLoaded event from firing until the script has loaded and finished evaluating.**

**Scripts with the defer attribute will execute in the order in which they appear in the document.**

**This attribute allows the elimination of parser-blocking JavaScript where the browser would have to load and evaluate scripts before continuing to parse. `async` has a similar effect in this case.**

For instance:

**The code in test.js:**

    function output() {
        console.log("execute javascript in test.js");
    }

    output();


```diff 
    <html>
    <head>   
- <script type="text/javascript" src="test.js"></script>
+ <script type="text/javascript" src="test.js" async defer></script>       
    </head>
    <body>
        Hello, World!
    <script>
        console.log("body render done.");
    </script>
    <body>
    </html>
``` 


    Without async and defer Output:
    execute javascript in test.js
    body render done.

    With async and defer Output:
    body render done.
    execute javascript in test.js

> [defer async](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script)