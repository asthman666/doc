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



