### Omit the protocol from embedded resources

Omit the protocol portion (http:, https:) from URLs pointing to images and other media files, style sheets, and scripts unless the respective files are not available over both protocols.

*Why?*: Omitting the protocol—which makes the URL relative—prevents mixed content issues and results in minor file size savings.

Not Recommended:
  ```html
  <script src="http://www.google.com/js/gweb/analytics/autotrack.js"></script>
  ```
  
Recommended:
  ```html
  <script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>
  ```

### Use correct document type

Always declare the document type as the first line in your document.

*Why?*: It defines which version of (X)HTML your document is actually using, and this is a critical piece of information needed by some tools processing the document.

  ```html
  <!doctype html>
  <!--rest of document -->
  ```


### Use only lowercase

All code should be lowercase: This applies to HTML element names, attributes, attribute values (unless text/CDATA), CSS selectors, properties, and property values (with the exception of strings).

*Why?*: Lowercase is a commonly used standard for attributes, and helps to keep code consistant.

Not Recommended:
  ```html
  <A HREF="/">Home</A>
  <input autoComplete />
  ```
  
Recommended:
  ```html
  <a href="/">Home</a>
  <input autocomplete />
  ```
  
### Quote all attribute values

Although quotes are optional for attribute values, always include them. Where a value includes a space then quoting is required for it to be valid, but always use them for single-word values too.

*Why?*: It helps to create consistancy throughout the document.

Not Recommended:
  ```html
  <td colspan=3></td>
  ```
  
Recommended:
  ```html
  <td colspan="3"></td>
  ```
  
### Indent by 4 spaces at a time

Don’t use tabs or mix tabs and spaces for indentation, and use four spaces for indentation.

*Why?*: Spaces are the only way to ensure that the document looks the same in any tool being used to view the source.

*Why?*: It helps to create consistancy throughout the document.

  ```html
  <div>
    <div>
      <p></p>
    </div>
  </div>
  ```


### Remove trailing white spaces

Never add trailing white space.

*Why?*: Trailing white spaces are unnecessary and can complicate diffs.

Not Recommended:
  ```html
  <p>What?_</p>
  <p>How?</p>_
  ```
  
Recommended:
  ```html
  <p>What?</p>
  <p>How?</p>
  ```

### Specify the correct encoding

Make sure your editor uses UTF-8 as character encoding, without a byte order mark. Specify the encoding in HTML templates and documents via <meta charset="utf-8">.

*Why?*: Specifying the encoding ensures that the code will be correctly parsed.


### Mark todos and action items with TODO

Highlight todos by using the keyword TODO only, not other common formats like @@.

*Why?*: Using a consistant format for todo comments makes them easy to find.

  ```html
  <!-- TODO: consider adding more options -->
  <ul>
    <li>Apples</li>
    <li>Oranges</li>
  </ul>
  ```


### Specify the correct document type

HTML5 (HTML syntax) is preferred for all HTML documents: <!DOCTYPE html>.
(It’s recommended to use HTML, as text/html. Do not use XHTML. XHTML, as application/xhtml+xml, lacks both browser and infrastructure support and offers less room for optimization than HTML.)

*Why?*: Specifying the document type ensures that the code will be correctly parsed.


### Always close void elements

Always close void elements, even though this is optional syntax.

*Why?*: Adding the trailing slash makes it obvious that the element can contain no children.

*Why?*: Although HTML5 introduced the optionality of the closing syntax, older types of XHTML require it.

Not Recommended:
  ```html
  <br>
  ```
  
Recommended:
  ```html
  <br />
  ```


### Use HTML according to its purpose

Use elements for what they have been created for. For example, use heading elements for headings, p elements for paragraphs, a elements for anchors, etc. Using HTML according to its purpose is important for accessibility, reuse, and code efficiency reasons.

*Why?*: Using proper elements shows clear intent with regards to the purpose of elements, and helps with generic styling.


Not Recommended:
  ```html
  <div onclick="goToRecommendations();">All recommendations</div>
  ```
  
Recommended:
  ```html
  <a href="recommendations/">All recommendations</a>
  ```


### Provide alternative contents for multimedia

For multimedia, such as images, videos, animated objects via canvas, make sure to offer alternative access. For images that means use of meaningful alternative text (alt) and for video and audio transcripts and captions, if available.

(For images whose alt attributes would introduce redundancy, and for images whose purpose is purely decorative which you cannot immediately use CSS for, use no alternative text, as in alt="".)

*Why?*: Providing alternative contents is important for accessibility reasons: A blind user has few cues to tell what an image is about without @alt, and other users may have no way of understanding what video or audio contents are about either.

Not Recommended:
  ```html
  <img src="spreadsheet.png">
  ```
  
Recommended:
  ```html
  <img src="spreadsheet.png" alt="Spreadsheet screenshot.">
  ```



### Separate structure from presentation from behavior

Strictly keep structure (markup), presentation (styling), and behavior (scripting) apart, and try to keep the interaction between the three to an absolute minimum. That is, make sure documents and templates contain only HTML and HTML that is solely serving structural purposes. Move everything presentational into style sheets, and everything behavioral into scripts.

In addition, keep the contact area as small as possible by linking as few style sheets and scripts as possible from documents and templates. Separating structure from presentation from behavior is important for maintenance reasons. 

*Why?*: It is always more expensive to change HTML documents and templates than it is to update style sheets and scripts.

*Why?*: Seperated files allow for more generic code to be shared by multiple documents.

Not Recommended:
  ```html
  <!DOCTYPE html>
  <title>HTML sucks</title>
  <link rel="stylesheet" href="base.css" media="screen">
  <link rel="stylesheet" href="grid.css" media="screen">
  <link rel="stylesheet" href="print.css" media="print">
  <h1 style="font-size: 1em;">HTML sucks</h1>
  <p>I’ve read about this on a few sites but now I’m sure:
    <u>HTML is stupid!!1</u>
  <center>I can’t believe there’s no way to control the styling of
    my website without doing everything all over again!</center>
  ```
  
Recommended:
  ```html
  <!DOCTYPE html>
  <title>My first CSS-only redesign</title>
  <link rel="stylesheet" href="default.css">
  <h1>My first CSS-only redesign</h1>
  <p>I’ve read about this on a few sites but today I’m actually
    doing it: separating concerns and avoiding anything in the HTML of
    my website that is presentational.</p>
  <p>It’s awesome!</p>
  ```


### Optional tags

Do not omit optional tags.

*Why?*: Including optional tags makes it very obvious to the reader the intent of the code.

Not Recommended:
  ```html
  <!DOCTYPE html>
  <title>Saving money, saving bytes</title>
  <p>Qed.
  ```
  
Recommended:
  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <title>Spending money, spending bytes</title>
    </head>
    <body>
      <p>Sic.</p>
    </body>
  </html>
  ```

### HTML comments

Format HTML lines consistently. Short comments should be written on one line. Long comments should be written with the opening and closing tags on sepatate lines, with indentation used for the text.

*Why?*: Using a consistant format helps with readability of the code.

*Why?*: Longer comments are easier to read when they are indented.

  ```html
  <!-- This is a short comment -->
  
  <!-- 
      This is a long comment example. This is a long comment example. This is a long comment example.
      This is a long comment example. This is a long comment example. This is a long comment example.
  -->
  ```


### Don't use entity references

There is no need to use entity references like &mdash;, &rdquo;, or &#x263a;, assuming the same encoding (UTF-8) is used for files and editors as well as among teams. The only exceptions apply to characters with special meaning in HTML (like < and &) as well as control or “invisible” characters (like no-break spaces).

*Why?*: Using the actual characters makes reading the code much easier.

Not Recommended:
  ```html
The currency symbol for the Euro is &ldquo;&eur;&rdquo;.
  ```
  
Recommended:
  ```html
  The currency symbol for the Euro is “€”.
  ```


### Omit type attributes for style sheets and scripts

Do not use type attributes for style sheets (unless not using CSS) and scripts (unless not using JavaScript).
Specifying type attributes in these contexts is not necessary as HTML5 implies text/css and text/javascript as defaults. This can be safely done even for older browsers.

*Why?*: Removing these unnessecary attributes keeps the code much more succinct, and reduceds the potential of getting them wrong.

Not Recommended:
  ```html
  <link rel="stylesheet" href="//www.google.com/css/maia.css" type="text/css">
  <script src="//www.google.com/js/gweb/analytics/autotrack.js" type="text/javascript"></script>
  ```
  
Recommended:
  ```html
  <link rel="stylesheet" href="//www.google.com/css/maia.css">
  <script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>
  ```


### Classes vs. IDs

You should only give elements an ID attribute if they are unique. They should be applied to that element only and nothing else. Classes can be applied to multiple elements that share the same style properties. Things that should look and work in the same way can have the same class name.

*Why?*: When elements are selected by id, there is an expectation that only a single element will be found.

  ```html
  <ul id="categories">
    <li class="item">Category 1</li>
    <li class="item">Category 2</li>
    <li class="item">Category 3</li>
  </ul>
  ```


### When quoting attributes values, use double quotation marks

Use double ("") rather than single quotation marks ('') around attribute values.

*Why?*: Using double quotation marks is a common standard used in HTML.

*Why?*: It is easier to include css statements in attributes, as these use single quotation marks, and therefore don't need to be escaped.

Not Recommended:
  ```html
  <a class='maia-button maia-button-secondary'>Sign in</a>
  ```
  
Recommended:
  ```html
  <a class="maia-button maia-button-secondary">Sign in</a>
  ```


### Spaces and equal signs

Spaces around equal signs is legal, but space-less is easier to read, and groups entities better together.

*Why?*: Pairs are much easier to identify when the spaces are omitted.

Not Recommended:
  ```html
  <link rel = "stylesheet" href = "styles.css">
  ```
  
Recommended:
  ```html
  <link rel="stylesheet" href="styles.css">
  ```


### Avoid long code lines

Try to avoid code lines longer than around 80 characters where appropriate.

*Why?*: When using an HTML editor, it is inconvenient to scroll right and left to read the HTML code.


### Specify both encoding and langage

Both the language and the character encoding should be defined as early as possible in a document.

*Why?*: This helps to ensure proper interpretation, and correct search engine indexing.

  ```html
  <!DOCTYPE html>
  <html lang="en-US">
  <head>
    <meta charset="UTF-8">
    <title>HTML5 Syntax and Coding Style</title>
  </head>
  ```


### Explain code as needed, where possible

Use comments to explain code: What does it cover, what purpose does it serve, why is respective solution used or preferred? This item is optional as it is not deemed a realistic expectation to always demand fully documented code. Mileage may vary heavily for HTML and CSS code and depends on the project’s complexity.

*Why?*: Comments can greatly help other maintainers of the code understand the intent and function.
