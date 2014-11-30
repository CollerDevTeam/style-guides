
Protocol
link ▽ Omit the protocol from embedded resources.
Omit the protocol portion (http:, https:) from URLs pointing to images and other media files, style sheets, and scripts unless the respective files are not available over both protocols.
Omitting the protocol—which makes the URL relative—prevents mixed content issues and results in minor file size savings.
/* Not recommended */
.example {
  background: url(http://www.google.com/images/example);
}
/* Recommended */
.example {
  background: url(//www.google.com/images/example);
}


Capitalization
Use only lowercase.
All code has to be lowercase: This applies to HTML element names, attributes, attribute values (unless text/CDATA), CSS selectors, properties, and property values (with the exception of strings).
/* Not recommended */
color: #E5E5E5;
/* Recommended */
color: #e5e5e5;


Trailing Whitespace
Remove trailing white spaces.
Trailing white spaces are unnecessary and can complicate diffs.
/* Not recommended */
color: #e5e5e5;_
/* Recommended */
color: #e5e5e5;


Encoding
Use UTF-8 (no BOM).
Make sure your editor uses UTF-8 as character encoding, without a byte order mark.
. Do not specify the encoding of style sheets as these assume UTF-8.

Comments
link ▽ Explain code as needed, where possible.
Use comments to explain code: What does it cover, what purpose does it serve, why is respective solution used or preferred?
(This item is optional as it is not deemed a realistic expectation to always demand fully documented code. Mileage may vary heavily for HTML and CSS code and depends on the project’s complexity.)

Action Items
link ▽ Mark todos and action items with TODO.
Highlight todos by using the keyword TODO only, not other common formats like @@.
/* TODO: example comment */
a {
}

ID and Class Naming
link ▽ Use meaningful or generic ID and class names.
Instead of presentational or cryptic names, always use ID and class names that reflect the purpose of the element in question, or that are otherwise generic.
Names that are specific and reflect the purpose of the element should be preferred as these are most understandable and the least likely to change.
Generic names are simply a fallback for elements that have no particular or no meaning different from their siblings. They are typically needed as “helpers.”
Using functional or generic names reduces the probability of unnecessary document or template changes.
/* Not recommended: meaningless */
#yee-1901 {}
/* Not recommended: presentational */
.button-green {}
.clear {}
/* Recommended: specific */
#gallery {}
#login {}
.video {}
/* Recommended: generic */
.aux {}
.alt {}

ID and Class Name Style
link ▽ Use ID and class names that are as short as possible but as long as necessary.
Try to convey what an ID or class is about while being as brief as possible.
Using ID and class names this way contributes to acceptable levels of understandability and code efficiency.
/* Not recommended */
#navigation {}
.atr {}
/* Recommended */
#nav {}
.author {}

Type Selectors
link ▽ Avoid qualifying ID and class names with type selectors.
Unless necessary (for example with helper classes), do not use element names in conjunction with IDs or classes.
Avoiding unnecessary ancestor selectors is useful for performance reasons.
/* Not recommended */
ul#example {}
div.error {}
/* Recommended */
#example {}
.error {}

Shorthand Properties
link ▽ Use shorthand properties where possible.
CSS offers a variety of shorthand properties (like font) that should be used whenever possible, even in cases where only one value is explicitly set.
Using shorthand properties is useful for code efficiency and understandability.
/* Not recommended */
border-top-style: none;
font-family: palatino, georgia, serif;
font-size: 100%;
line-height: 1.6;
padding-bottom: 2em;
padding-left: 1em;
padding-right: 1em;
padding-top: 0;
/* Recommended */
border-top: 0;
font: 100%/1.6 palatino, georgia, serif;
padding: 0 1em 2em;

0 and Units
link ▽ Omit unit specification after “0” values.
Do not use units after 0 values unless they are required.
margin: 0;
padding: 0;

Leading 0s
link ▽ Omit leading “0”s in values.
Do not use put 0s in front of values or lengths between -1 and 1.
font-size: .8em;

Hexadecimal Notation
link ▽ Use 3 character hexadecimal notation where possible.
For color values that permit it, 3 character hexadecimal notation is shorter and more succinct.
/* Not recommended */
color: #eebbcc;
/* Recommended */
color: #ebc;

ID and Class Name Delimiters
link ▽ Separate words in ID and class names by a hyphen.
Do not concatenate words and abbreviations in selectors by any characters (including none at all) other than hyphens, in order to improve understanding and scannability.
/* Not recommended: does not separate the words “demo” and “image” */
.demoimage {}
/* Not recommended: uses underscore instead of hyphen */
.error_status {}
/* Recommended */
#video-id {}
.ads-sample {}

Hacks
link ▽ Avoid user agent detection as well as CSS “hacks”—try a different approach first.
It’s tempting to address styling differences over user agent detection or special CSS filters, workarounds, and hacks. Both approaches should be considered last resort in order to achieve and maintain an efficient and manageable code base. Put another way, giving detection and hacks a free pass will hurt projects in the long run as projects tend to take the way of least resistance. That is, allowing and making it easy to use detection and hacks means using detection and hacks more frequently—and more frequently is too frequently.

Declaration Order
link ▽ Alphabetize declarations.
Put declarations in alphabetical order in order to achieve consistent code in a way that is easy to remember and maintain.
Ignore vendor-specific prefixes for sorting purposes. However, multiple vendor-specific prefixes for a certain CSS property should be kept sorted (e.g. -moz prefix comes before -webkit).
/* example */
background: fuchsia;
border: 1px solid;
-moz-border-radius: 4px;
-webkit-border-radius: 4px;
border-radius: 4px;
color: black;
text-align: center;
text-indent: 2em;

Block Content Indentation
link ▽ Indent all block content.
Indent all block content, that is rules within rules as well as declarations, so to reflect hierarchy and improve understanding.
@media screen, projection {
  html {
    background: #fff;
    color: #444;
  }
}

Declaration Stops
link ▽ Use a semicolon after every declaration.
End every declaration with a semicolon for consistency and extensibility reasons.
/* Not recommended */
.test {
  display: block;
  height: 100px
}
/* Recommended */
.test {
  display: block;
  height: 100px;
}

Property Name Stops
link ▽ Use a space after a property name’s colon.
Always use a single space between property and value (but no space between property and colon) for consistency reasons.
/* Not recommended */
h3 {
  font-weight:bold;
}
/* Recommended */
h3 {
  font-weight: bold;
}

Declaration Block Separation
link ▽ Use a space between the last selector and the declaration block.
Always use a single space between the last selector and the opening brace that begins the declaration block.
The opening brace should be on the same line as the last selector in a given rule.
/* Not recommended: missing space */
#video{
  margin-top: 1em;
}
/* Not recommended: unnecessary line break */
#video
{
  margin-top: 1em;
}
/* Recommended */
#video {
  margin-top: 1em;
}


Selector and Declaration Separation
link ▽ Separate selectors and declarations by new lines.
Always start a new line for each selector and declaration.
/* Not recommended */
a:focus, a:active {
  position: relative; top: 1px;
}
/* Recommended */
h1,
h2,
h3 {
  font-weight: normal;
  line-height: 1.2;
}


Rule Separation
link ▽ Separate rules by new lines.
Always put a blank line (two line breaks) between rules.
html {
  background: #fff;
}
body {
  margin: auto;
  width: 50%;
}

CSS Quotation Marks
link ▽ Use single quotation marks for attribute selectors and property values.
Use single ('') rather than double ("") quotation marks for attribute selectors or property values. Do not use quotation marks in URI values (url()).
Exception: If you do need to use the @charset rule, use double quotation marks—single quotation marks are not permitted.
/* Not recommended */
@import url("//www.google.com/css/maia.css");
html {
  font-family: "open sans", arial, sans-serif;
}
/* Recommended */
@import url(//www.google.com/css/maia.css);
html {
  font-family: 'open sans', arial, sans-serif;
}

Section Comments
link ▽ Group sections by a section comment (optional).
If possible, group style sheet sections together by using comments. Separate sections with new lines.
/* Header */
#adw-header {}
/* Footer */
#adw-footer {}
/* Gallery */
.adw-gallery {}


avoid the use of !important
Using !important overrides all specificity no matter how high it is. We like to avoid using it for this reason. Most of the time it is not necessary. Even if you need to override a selector in a stylesheet you don't have access to, there are usually ways to override it without using !important. Avoid using it if possible.

ems/pxls