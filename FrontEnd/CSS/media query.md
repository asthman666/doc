Put this meta tag in your html head:

    <meta name="viewport" content="width=device-width, minimum-scale=1.0, maximum-scale=1.0" />

1. Here is an example of a max-width query.

        @media only screen and (max-width: 600px)  {...}

    What this query really means, is “If [device width] is **less than or equal** to 600px, then do {…}”

2. Here is an example of a min-width query.

        @media only screen and (min-width: 600px)  {...}

    What this query really means, is “If [device width] is **greater than or equal** to 600px, then do {…}”


Test Code:

    <html>
    <head>
    <meta name="viewport" content="width=device-width, minimum-scale=1.0, maximum-scale=1.0" />
    <style>
    .visible-mobile {
    display: none;
    }

    .visible-desktop {
        display: inline;
    }

    @media only screen and (max-width: 767px) {
    .visible-mobile {
        display: inline;
    }
    .visible-desktop {
        display: none;
    }
    }
    </style>
    <script>
    function cc() {
        alert("call js submit");
        document.querySelector("#formtest").submit();
    }
    </script>
    </head>
    <body>
    <form method="get" id="formtest">
    <input type="text" name="name" placeholder="Please input your name">
    <input type="button" onclick="cc();" value="search-button" class="visible-desktop">
    <input type="submit" onclick="cc();" value="search-submit" class="visible-mobile">
    </form>
    </body>
    </html>


> [min-width_and_max-width](https://www.emailonacid.com/blog/article/email-development/emailology_media_queries_demystified_min-width_and_max-width/)


>[Using media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries)

> [what-is-the-difference-between-screen-and-only-screen-in-media-queries](https://stackoverflow.com/questions/8549529/what-is-the-difference-between-screen-and-only-screen-in-media-queries)

