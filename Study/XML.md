## What are the special characters in XML?

**Just five:** `&lt; (<), &amp; (&), &gt; (>), &quot; ("), and &apos; (')`.

If your keyboard will not allow you to type the characters you want, or if you want to use characters outside the limits of the encoding scheme you have chosen, you can use a symbolic notation called ‘entity referencing’. Entity references can either be numeric, using the decimal or hexadecimal Unicode code point for the character (eg if your keyboard has no Euro symbol (€) you can type &#8364;); or they can be character, using an established set of names which you can declare in your DTD (eg <!ENTITY euro "&#8364;">) which then lets you use the name &euro; in your document. If you are using a Schema, you must use the numeric form for all except the five below because Schemas have no way to make character entity declarations.

> [specials](http://xml.silmaril.ie/specials.html)
