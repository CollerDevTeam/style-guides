Indentation
(Readability vs Compression)

Protocol
link ▽ Omit the protocol from embedded resources.
Omit the protocol portion (http:, https:) from URLs pointing to images and other media files, style sheets, and scripts unless the respective files are not available over both protocols.
Omitting the protocol—which makes the URL relative—prevents mixed content issues and results in minor file size savings.
<!-- Not recommended -->
<script src="http://www.google.com/js/gweb/analytics/autotrack.js"></script>
<!-- Recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>


Use Correct Document Type
Always declare the document type as the first line in your document:
<!doctype html>

Use Lower Case Attribute Names

Quote all Attribute Values


Indentation
link ▽ Indent by 2 spaces at a time.
Don’t use tabs or mix tabs and spaces for indentation.

Capitalization
Use only lowercase.
All code has to be lowercase: This applies to HTML element names, attributes, attribute values (unless text/CDATA), CSS selectors, properties, and property values (with the exception of strings).
<!-- Not recommended -->
<A HREF="/">Home</A>
<!-- Recommended -->
<img src="google.png" alt="Google">

Trailing Whitespace
Remove trailing white spaces.
Trailing white spaces are unnecessary and can complicate diffs.
<!-- Not recommended -->
<p>What?_
<!-- Recommended -->
<p>Yes please.

Encoding
Use UTF-8 (no BOM).
Make sure your editor uses UTF-8 as character encoding, without a byte order mark.
Specify the encoding in HTML templates and documents via <meta charset="utf-8">.

Comments
link ▽ Explain code as needed, where possible.
Use comments to explain code: What does it cover, what purpose does it serve, why is respective solution used or preferred?
(This item is optional as it is not deemed a realistic expectation to always demand fully documented code. Mileage may vary heavily for HTML and CSS code and depends on the project’s complexity.)

Action Items
link ▽ Mark todos and action items with TODO.
Highlight todos by using the keyword TODO only, not other common formats like @@.
<!-- TODO: remove optional tags -->
<ul>
  <li>Apples</li>
  <li>Oranges</li>
</ul>


Document Type
link ▽ Use HTML5.
HTML5 (HTML syntax) is preferred for all HTML documents: <!DOCTYPE html>.
(It’s recommended to use HTML, as text/html. Do not use XHTML. XHTML, as application/xhtml+xml, lacks both browser and infrastructure support and offers less room for optimization than HTML.)

Always close void elements, so that it is obvious that these do not contain any content, i.e. write <br />, not <br>.


Semantics
link ▽ Use HTML according to its purpose.
Use elements (sometimes incorrectly called “tags”) for what they have been created for. For example, use heading elements for headings, p elements for paragraphs, a elements for anchors, etc.
Using HTML according to its purpose is important for accessibility, reuse, and code efficiency reasons.
<!-- Not recommended -->
<div onclick="goToRecommendations();">All recommendations</div>
<!-- Recommended -->
<a href="recommendations/">All recommendations</a>

Multimedia Fallback
link ▽ Provide alternative contents for multimedia.
For multimedia, such as images, videos, animated objects via canvas, make sure to offer alternative access. For images that means use of meaningful alternative text (alt) and for video and audio transcripts and captions, if available.
Providing alternative contents is important for accessibility reasons: A blind user has few cues to tell what an image is about without @alt, and other users may have no way of understanding what video or audio contents are about either.
(For images whose alt attributes would introduce redundancy, and for images whose purpose is purely decorative which you cannot immediately use CSS for, use no alternative text, as in alt="".)
<!-- Not recommended -->
<img src="spreadsheet.png">
<!-- Recommended -->
<img src="spreadsheet.png" alt="Spreadsheet screenshot.">

Separation of Concerns
link ▽ Separate structure from presentation from behavior.
Strictly keep structure (markup), presentation (styling), and behavior (scripting) apart, and try to keep the interaction between the three to an absolute minimum.
That is, make sure documents and templates contain only HTML and HTML that is solely serving structural purposes. Move everything presentational into style sheets, and everything behavioral into scripts.
In addition, keep the contact area as small as possible by linking as few style sheets and scripts as possible from documents and templates.
Separating structure from presentation from behavior is important for maintenance reasons. It is always more expensive to change HTML documents and templates than it is to update style sheets and scripts.
<!-- Not recommended -->
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
<!-- Recommended -->
<!DOCTYPE html>
<title>My first CSS-only redesign</title>
<link rel="stylesheet" href="default.css">
<h1>My first CSS-only redesign</h1>
<p>I’ve read about this on a few sites but today I’m actually
  doing it: separating concerns and avoiding anything in the HTML of
  my website that is presentational.</p>
<p>It’s awesome!</p>



Entity References
link ▽ Do not use entity references.
There is no need to use entity references like &mdash;, &rdquo;, or &#x263a;, assuming the same encoding (UTF-8) is used for files and editors as well as among teams.
The only exceptions apply to characters with special meaning in HTML (like < and &) as well as control or “invisible” characters (like no-break spaces).
<!-- Not recommended -->
The currency symbol for the Euro is &ldquo;&eur;&rdquo;.
<!-- Recommended -->
The currency symbol for the Euro is “€”.


Optional Tags
link ▽ Omit optional tags (optional).
Consider including optional tags for better readability of the code.
<!-- Not recommended -->
<!DOCTYPE html>
<title>Saving money, saving bytes</title>
<p>Qed.
<!-- Recommended -->
<!DOCTYPE html>
<html>
  <head>
    <title>Spending money, spending bytes</title>
  </head>
  <body>
    <p>Sic.</p>
  </body>
</html>


type Attributes
link ▽ Omit type attributes for style sheets and scripts.
Do not use type attributes for style sheets (unless not using CSS) and scripts (unless not using JavaScript).
Specifying type attributes in these contexts is not necessary as HTML5 implies text/css and text/javascript as defaults. This can be safely done even for older browsers.
<!-- Not recommended -->
<link rel="stylesheet" href="//www.google.com/css/maia.css"
  type="text/css">
<!-- Recommended -->
<link rel="stylesheet" href="//www.google.com/css/maia.css">
<!-- Not recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"
  type="text/javascript"></script>
<!-- Recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>


General Formatting
link ▽ Use a new line for every block, list, or table element, and indent every such child element.
Independent of the styling of an element (as CSS allows elements to assume a different role per display property), put every block, list, or table element on a new line.
Also, indent them if they are child elements of a block, list, or table element.
(If you run into issues around whitespace between list items it’s acceptable to put all li elements in one line. A linter is encouraged to throw a warning instead of an error.)
<blockquote>
  <p><em>Space</em>, the final frontier.</p>
</blockquote>
<ul>
  <li>Moe
  <li>Larry
  <li>Curly
</ul>
<table>
  <thead>
    <tr>
      <th scope="col">Income
      <th scope="col">Taxes
  <tbody>
    <tr>
      <td>$ 5.00
      <td>$ 4.50
</table>

HTML Quotation Marks
link ▽ When quoting attributes values, use double quotation marks.
Use double ("") rather than single quotation marks ('') around attribute values.
<!-- Not recommended -->
<a class='maia-button maia-button-secondary'>Sign in</a>
<!-- Recommended -->
<a class="maia-button maia-button-secondary">Sign in</a>


Spaces and Equal Signs
Spaces around equal signs is legal:
<link rel = "stylesheet" href = "styles.css">
But space-less is easier to read, and groups entities better together:
<link rel="stylesheet" href="styles.css">



Avoid Long Code Lines
When using an HTML editor, it is inconvenient to scroll right and left to read the HTML code.
Try to avoid code lines longer than 80 characters.



To ensure proper interpretation, and correct search engine indexing, both the language and the character encoding should be defined as early as possible in a document:
<!DOCTYPE html>
<html lang="en-US">
<head>
  <meta charset="UTF-8">
  <title>HTML5 Syntax and Coding Style</title>
</head>


HTML Comments
Short comments should be written on one line, with a space after <!-- and a space before -->:
<!-- This is a comment -->
Long comments, spanning many lines, should be written with <!-- and --> on separate lines:
<!-- 
  This is a long comment example. This is a long comment example. This is a long comment example.
  This is a long comment example. This is a long comment example. This is a long comment example.
-->
Long comments are easier to observe, if they are indented 2 spaces.


Classes vs. IDs◊
You should only give elements an ID attribute if they are unique. They should be applied to that element only and nothing else. Classes can be applied to multiple elements that share the same style properties. Things that should look and work in the same way can have the same class name.
1.
<ul id="categories">
2.
<li class="item">Category 1</li>
3.
<li class="item">Category 2</li>
4.
<li class="item">Category 3</li>
5.
</ul>


