

    <html>
    <head>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js" type="text/javascript"></script>
    <script>
        $(function() {
            $("#btn").on("click", function(){
                alert(2);
                return false;
            });
            // $("#btn").on("click", function(){
            //     alert(3);
            //     return true;
            // });
        })
    </script>
    </head>
    <body>
    <form>
    <input id="btn" type="submit" onclick="javascript:alert(1);" value="submit">
    </form>
    </body>
    </html>