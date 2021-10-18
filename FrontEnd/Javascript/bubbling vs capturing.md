The basic problem is very simple. Suppose you have a element inside an element

    -----------------------------------
    | element1                        |
    |   -------------------------     |
    |   |element2               |     |
    |   -------------------------     |
    |                                 |
    -----------------------------------

and both have an onClick event handler. If the user clicks on element2 he causes a click event in both element1 and element2. But which event fires first? Which event handler should be executed first? What, in other words, is the event order?

### Two models
Not surprisingly, back in the bad old days Netscape and Microsoft came to different conclusions.

* Netscape said that the event on element1 takes place first. This is called event capturing.
* Microsoft maintained that the event on element2 takes precedence. This is called event bubbling.

[Event order](https://www.quirksmode.org/js/events_order.html)