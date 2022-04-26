## HTML5

The term HTML5 is essentially a buzzword that refers to a set of modern web technologies. This includes the HTML Living Standard, along with JavaScript APIs to enhance storage, multimedia, and hardware access.

Any modern site should use the HTML doctype — this will ensure that you are using the latest version of HTML.

### Doctype(HTML5 doctype)

You should use the HTML5 doctype. It is short, easy to remember, and backwards compatible:

    <!DOCTYPE html>

### Document language

Set the document language using the lang attribute on your <html> element:

    <html lang="en-US">

This is good for accessibility and search engines, helps with localizing content, and reminds people to use best practices.    
### Document characterset

    <meta charset="utf-8">

 In addition, you should always specify the characterset as early as possible within your HTML's `<head>` block (within the first kilobyte), as it protects against a rather nasty Internet Explorer security vulnerability    

### Viewport meta tag

Finally, you should always add the viewport meta tag into your HTML `<head>`, to give the example a better chance of working on mobile devices. You should include at least the following in your document, which can be modified later on as the need arises:

    <meta name="viewport" content="width=device-width">

[General markup coding style](https://developer.mozilla.org/en-US/docs/MDN/Guidelines/Code_guidelines/HTML#general_markup_coding_style)

