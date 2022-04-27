# prototype (原型)

    if (!String.prototype.trim) {
        String.prototype.trim = function () {
            return this.replace(/^[\s\uFEFF\xA0]+|[\s\uFEFF\xA0]+$/g, '');
        };
    }

> [prototypes](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes)

> [object-defineproperty-or-prototype](https://stackoverflow.com/questions/38961414/object-defineproperty-or-prototype)

> [for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)

> [object-methods](http://es6.ruanyifeng.com/?search=prototype&x=7&y=10#docs/object-methods)

> [extension method javascript](https://stackoverflow.com/questions/9354298/how-do-i-write-an-extension-method-in-javascript)

> [trim](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/trim)