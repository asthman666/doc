The `DOMContentLoaded` event fires when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading.

The `load` event is fired when the whole page has loaded, including all dependent resources such as stylesheets and images.

> [DOMContentLoaded](https://developer.mozilla.org/en-US/docs/Web/API/Window/DOMContentLoaded_event)

> [load](https://developer.mozilla.org/en-US/docs/Web/API/Window/load_event)


For instance:

    <html>
    <head>
    <script>
        window.addEventListener('DOMContentLoaded', (event) => {
            console.log('DOM fully loaded and parsed except stylesheets, images, and subframes.');
        });
        window.addEventListener('load', (event) => {
            console.log('DOM fully loaded and parsed.');
        });
    </script>
    </head>
    <body>
        Hello, World!
    <script>
        console.log("body render done.");
    </script>
    <body>
    </html>

    // The output will be:
    // body render done.
    // DOM fully loaded and parsed except stylesheets, images, and subframes.
    // DOM fully loaded and parsed.