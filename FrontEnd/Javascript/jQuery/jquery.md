# JQuery

    // deprecated as of jQuery 1.8 and removed in jQuery 3.0.
    $(document).ready(function () { ... })

    // shorthand for $(document).ready()
    $(function() { ... })

    // run jQuery in compatibility mode with other libraries,
    jQuery(function ($) {
        // use $ here
    });

    // window onload event
    $( window ).load(function () { ... })

    $( window ).on( "load", function() { ... })

    // window resize event
    $(window).resize(function () {})

    // pass nothing to function
    (function () {
        ...
    })()

    // pass window.jQuery and window to function
    (function ($, window) {
        ...
    })(window.jQuery, window)

> [document ready-window load](https://stackoverflow.com/questions/4584373/difference-between-window-load-and-document-ready-functions)

> [selected from dropdown](https://stackoverflow.com/questions/10659097/jquery-get-selected-option-from-dropdown)

> [document-ready](http://learn.jquery.com/using-jquery-core/document-ready/)