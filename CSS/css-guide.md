### Omit the protocol from embedded resources

Omit the protocol portion (http:, https:) from URLs pointing to images and other media files, style sheets, and scripts unless the respective files are not available over both protocols.

*Why?*: Omitting the protocol—which makes the URL relative—prevents mixed content issues and results in minor file size savings.

Not Recommended:
  ```css
  .example {
    background: url(http://www.google.com/images/example);
  }
  ```
  
Recommended:
  ```css
  .example {
    background: url(//www.google.com/images/example);
  }
  ```


### Use only lowercase

All code should be lowercase: This applies to CSS selectors, properties, and property values (with the exception of strings).

*Why?*: Lowercase is a commonly used standard for attributes, and helps to create consistency throughout the code. 

Not Recommended:
  ```css
  color: #E5E5E5;
  ```
  
Recommended:
  ```css
  color: #e5e5e5;
  ```


### Remove trailing white spaces

Never add trailing white space.

*Why?*: Trailing white spaces are unnecessary and can complicate diffs.

Not Recommended:
  ```css
  color: #e5e5e5;_
  ```
  
Recommended:
  ```css
  color: #e5e5e5;
  ```
  

### Encoding

Do not specify the encoding - style sheets assume the use of UTF-8.

*Why?*: Omitting the encoding reduces the potential to set it incorrectly.


### Explain code as needed, where possible

Use comments to explain code: What does it cover, what purpose does it serve, why is respective solution used or preferred?
This item is optional as it is not deemed a realistic expectation to always demand fully documented code. Mileage may vary heavily for HTML and CSS code and depends on the project’s complexity.

*Why?*: Comments can greatly help other maintainers of the code understand the intent and function.


### Mark todos and action items with TODO

Highlight todos by using the keyword TODO only, not other common formats like @@.

*Why?*: Using a consistant format for todo comments makes them easy to find.

  ```css
  /* TODO: example comment */
  a {
  }
  ```

### Use meaningful or generic ID and class names

Instead of presentational or cryptic names, always use ID and class names that reflect the purpose of the element in question, or that are otherwise generic. Names that are specific and reflect the purpose of the element should be preferred as these are most understandable and the least likely to change.

Generic names are simply a fallback for elements that have no particular or no meaning different from their siblings. They are typically needed as “helpers.” 

*Why?*: Using functional or generic names reduces the probability of unnecessary document or template changes.

Not Recommended (presentational):
  ```css
  .button-green {}
  .clear {}
  ```

Recommended (specific):
  ```css
  #gallery {}
  #login {}
  ```
  
Recommended (generic):
  ```css
  .aux {}
  .alt {}
  ```


### ID and Class Name Style

Use ID and class names that are as short as possible but as long as necessary. Try to convey what an ID or class is about while being as brief as possible.

*Why?*: Using ID and class names this way contributes to acceptable levels of understandability and code efficiency.

Not Recommended:
  ```css
  #navigation {}
  .atr {}
  ```
  
Recommended:
  ```css
  #nav {}
  .author {}
  ```


### Avoid qualifying ID and class names with type selectors

Unless necessary (for example with helper classes), do not use element names in conjunction with IDs or classes.

*Why?*: Avoiding unnecessary ancestor selectors is useful for performance reasons.

Not Recommended:
  ```css
  ul#example {}
  div.error {}
  ```
  
Recommended:
  ```css
  #example {}
  .error {}
  ```


### Use shorthand properties where possible

CSS offers a variety of shorthand properties (like font) that should be used whenever possible, even in cases where only one value is explicitly set.

*Why?*: Using shorthand properties is useful for code efficiency and understandability (through grouping).

Not Recommended:
  ```css
  border-top-style: none;
  font-family: palatino, georgia, serif;
  font-size: 100%;
  line-height: 1.6;
  padding-bottom: 2em;
  padding-left: 1em;
  padding-right: 1em;
  padding-top: 0;
  ```
  
Recommended:
  ```css
  border-top: 0;
  font: 100%/1.6 palatino, georgia, serif;
  padding: 0 1em 2em;
  ```


### Omit unit specification after “0” values

Do not use units after 0 values unless they are required.

*Why?*: Units don't apply to '0', and omitting them helps with readability, and minor file size shavings.

Not Recommended:
  ```css
  margin: 0em;
  padding: 1px 0px 1px 2px;
  ```
  
Recommended:
  ```css
  margin: 0;
  padding: 1px 0 1px 2px;
  ```


### Add leading “0”s to values

Use 0s in front of values or lengths between -1 and 1.

*Why?*: It makes it clear at a glance that the value is a decimal.

Not Recommended:
  ```css
  font-size: .8em;
  ```
  
Recommended:
  ```css
  font-size: 0.8em;
  ```


### Use short hexadecimal notation where possible

For color values that permit it, use a 3 character hex notation where possible

*Why?*: 3 character hexadecimal notation is shorter and more succinct.

Not Recommended:
  ```css
  color: #eebbcc;
  ```
  
Recommended:
  ```css
  color: #ebc;
  ```
  

### Separate words in ID and class names by a hyphen

Do not concatenate words and abbreviations in selectors by any characters (including none at all) other than hyphens

*Why?*: It improves understanding and scannability.

Not Recommended:
  ```css
  #demoimage {}
  .error_status {}
  ```
  
Recommended:
  ```css
  #demo-image {}
  .error-status {}
  ```


### Avoid common CSS 'hacks'

It’s tempting to address styling differences over user agent detection or special CSS filters, workarounds, and hacks. Both approaches should be considered last resort in order to achieve and maintain an efficient and manageable code base.

*Why?*: Giving hacks a free pass will hurt projects in the long run as projects tend to take the way of least resistance.


### Alphabetize declarations

Put declarations in alphabetical order in order to achieve consistent code in a way that is easy to remember and maintain. Ignore vendor-specific prefixes for sorting purposes. However, multiple vendor-specific prefixes for a certain CSS property should be kept sorted (e.g. -moz prefix comes before -webkit).

*Why?*: The consistent order helps when comparing styles between matchers.

  ```css
  background: fuchsia;
  border: 1px solid;
  -moz-border-radius: 4px;
  -webkit-border-radius: 4px;
  border-radius: 4px;
  color: black;
  text-align: center;
  text-indent: 2em;
  ```


### Indent all block content

Indent all block content, that is rules within rules as well as declarations.

*Why?*: The helps to reflect hierarchy and improve understanding.

  ```css
  @media screen, projection {
    html {
      background: #fff;
      color: #444;
    }
  }
  ```


### Use a semicolon after every declaration

End every declaration with a semicolon.

*Why?*: The helps to promote consistancy, and makes extending the code easier.

Not Recommended:
  ```css
  .test {
    display: block;
    height: 100px
  }
  ```
  
Recommended:
  ```css
  .test {
    display: block;
    height: 100px;
  }
  ```


### Use a space after a property name’s colon

Always use a single space between property and value (but no space between property and colon).

*Why?*: The helps to promote consistancy, and makes reading (and comparing) the code easier.

Not Recommended:
  ```css
  h3 {
    font-weight:bold;
  }
  ```
  
Recommended:
  ```css
  h3 {
    font-weight: bold;
  }
  ```


### Use a space between the last selector and the declaration block

Always use a single space between the last selector and the opening brace that begins the declaration block. The opening brace should be on the same line as the last selector in a given rule.

*Why?*: The helps to promote consistancy, and makes reading (and comparing) the code easier.

Not Recommended (missing space):
  ```css
  #video{
    margin-top: 1em;
  }
  ```

Not Recommended (unnecessary line break):
  ```css
  #video
  {
    margin-top: 1em;
  }
  ```

Recommended:
  ```css
  #video {
    margin-top: 1em;
  }
  ```


### Separate selectors and declarations by new lines

Always start a new line for each selector and declaration.

*Why?*: It is more clear at a glance which selectors are being targeted.

Not Recommended:
  ```css
  a:focus, a:active {
    position: relative; top: 1px;
  }
  ```

Recommended:
  ```css
  h1,
  h2,
  h3 {
    font-weight: normal;
    line-height: 1.2;
  }
  ```


### Separate rules by new lines

Always put a blank line (two line breaks) between rules.

*Why?*: The helps to promote consistancy, and makes reading (and comparing) the code easier.

Not Recommended:
  ```css
  body {
    margin: auto;
  }
  h1 {
    font-size: 1em;
  }
  ```

Recommended:
  ```css
  body {
    margin: auto;
  }
  
  h1 {
    font-size: 1em;
  }
  ```


### Use single quotation marks for attribute selectors and property values

Use single ('') rather than double ("") quotation marks for attribute selectors or property values. Do not use quotation marks in URI values (url()). An exception is if you do need to use the @charset rule, then use double quotation marks—single quotation marks are not permitted.

*Why?*: Single quotation marks are the standard supported by CSS.

Not Recommended:
  ```css
  @import url("//www.google.com/css/maia.css");
  html {
    font-family: "open sans", arial, sans-serif;
  }
  ```

Recommended:
  ```css
  @import url(//www.google.com/css/maia.css);
  html {
    font-family: 'open sans', arial, sans-serif;
  }
  ```


### Section comments

If possible, group style sheet sections together by using comments. Separate sections with two blank lines.

*Why?*: This helps to visually group selectors together, and also provides a name / brief description of the related section.

  ```css
  /* Header */

  #adw-header {}


  /* Footer */

  #adw-footer {}


  /* Gallery */

  .adw-gallery {}
  ```


### Avoid the use of !important

Using !important overrides all specificity no matter how high it is. We like to avoid using it for this reason. Most of the time it is not necessary. Even if you need to override a selector in a stylesheet you don't have access to, there are usually ways to override it without using !important. Avoid using it if possible.

*Why?*: It breaks the intent of any other rules, and is promotes bad design.


### Avoid using inline styles

All CSS should be in a stylesheet file - we should not use inline styles in HTML. 

*Why?*: Inline styles make it much harder to make broad changes, and generally indicate a wider problem in the css rules.


Not Recommended:
  ```css
  <div style="height: 50px;"></div>
  ```
