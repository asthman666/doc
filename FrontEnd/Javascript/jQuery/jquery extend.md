> [extend](https://api.jquery.com/jquery.extend/)

> [fn.extend](https://api.jquery.com/jquery.fn.extend/)

> [difference-between-jquery-extend-and-jquery-fn-extend](https://stackoverflow.com/questions/1991126/difference-between-jquery-extend-and-jquery-fn-extend)


    jQuery.extend({
        abc: function(){
            alert('abc');
        }
    });

usage: `$.abc()`. (No selector required like `$.ajax()`.)

    jQuery.fn.extend({
        xyz: function(){
            alert('xyz');
        }
    });
usage: `$('.selector').xyz()`. (Selector required like $`('#button').click()`.)