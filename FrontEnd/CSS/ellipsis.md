# ellipsis

## Ellipsis for Single Line Text

* must have a width, max-width or flex-basis
* must have white-space: nowrap
* must have overflow with value other than visible
* must be display: block or inline-block (or the functional equivalent, such as a flex item).

例如:

    p {
        width: 100px;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
        border: 1px solid #ddd;
        margin: 0;
    }

[codepen](https://codepen.io/asthman666/pen/KLomQK)

> [Applying an ellipsis to multiline text](https://stackoverflow.com/questions/33058004/applying-an-ellipsis-to-multiline-text)