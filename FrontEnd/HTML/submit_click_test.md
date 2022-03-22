

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

When clicking the `submit` button or focusing on Name input box and click Enter key, will alert(1) first, alert(2) second and will not submit the form because of the `return false`.

Uncomment the code and code will become:

    <html>
    <head>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js" type="text/javascript"></script>
    <script>
        $(function() {
            $("#btn").on("click", function(){
                alert(2);
                return false;
            });
            $("#btn").on("click", function(){
                alert(3);
                return true;
            });
        })
    </script>
    </head>
    <body>
    <form>
        <label>Name:<input type="text" value="" name="name"></label>
        <input id="btn" type="submit" onclick="javascript:alert(1);" value="submit">
    </form>
    </body>
    </html>

When clicking the `submit` button or focusing on Name input box and click Enter key, will alert(1) first, alert(2) second, alert(3) third and will not submit the form because of the `return false`.