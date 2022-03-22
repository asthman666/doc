## input type button vs submit

`<input type="button" />` buttons will not submit a form - they don't do anything by default. They're generally used in conjunction with JavaScript as part of an AJAX application.

`<input type="submit" />` buttons will submit the form they are in when the user clicks on them, unless you specify otherwise with JavaScript.

### Notes:
* Also browsers can capture the "Enter" keypress on a form and submit the form automatically if there is a submit button, but not otherwise.

## button

`autocomplete`

This attribute on a `<button>` is nonstandard and Firefox-specific. Unlike other browsers, Firefox persists the dynamic disabled state of a `<button>` across page loads. Setting autocomplete="off" on the button disables this feature; see bug 654072. **This bug also exists in `<input type='submit' />` or `<input type='button' />`.**

`type`

submit: The button submits the form data to the server. This is the **default** if the attribute is not specified for buttons associated with a `<form>`, or if the attribute is an empty or invalid value.

reset: The button resets all the controls to their initial values, like `<input type="reset">`. (This behavior tends to annoy users.)

button: The button has no default behavior, and does nothing when pressed by default. It can have client-side scripts listen to the element's events, which are triggered when the events occur.

### Notes:
* Buttons created with the BUTTON element function just like buttons created with the INPUT element, but they offer richer rendering possibilities. Inside a `<button>` element you can put content, like text or images.

