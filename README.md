# HTML, CSS, and LESS code guide
Standards for developing flexible, durable, and sustainable HTML, CSS, and LESS.



----------



## Table of contents

* [Golden rule](#golden-rule)
* [HTML](#html)
    * [Syntax](#html-syntax)
    * [HTML5 doctype](#html5-doctype)
    * [Pragmatism over semantics](#pragmatism-over-semantics)
    * [Attribute order](#attribute-order)
    * [Boolean attributes](#boolean-attributes)
    * [JavaScript generated markup](#javascript-generated markup)
* [CSS](#css)
    * [CSS syntax](#css-syntax)
    * [Declaration order](#declaration-order)
    * [Formatting exceptions](#formatting-exceptions)
        * [Prefixed properties](#prefixed-properties)
        * [Rules with single declarations](#rules-with-single-declarations)
    * [Human readable](#human-readable)
        * [Comments](#comments)
        * [Classes](#classes)
        * [Selectors](#selectors)
    * [Organization](#organization)
* [LESS](#less)
    * [File naming and directory structure](#file-naming-and-directory-structure)
    * [Variable and Mixins](#variables-and-mixins)
    * [Standard variable and mixin abbreviations](#standard-variable-and-mixin-abbreviations)
* [Utility suffix definitions](#utility-suffix-definitions)
    * [Container](#container)
    * [Wrapper](#wrapper)
    * [Sidebar and Content](#sidebar-and-content)
    * [Header, Body, and Footer](#header-body-and-footer)
* [Writing copy](#copy)
    * [Sentence case](#sentence-case)



----------



## Golden rule

> All code in any code base should look like a single person typed it, no matter how many people contributed.

This means strictly enforcing these agreed upon guidelines at all times. For additions or contributions, please [file an issue on GitHub](https://github.com/nemophrost/code-guide).



----------



## HTML


### HTML syntax

* Use hard-tabs
* Nested elements should be indented once (1 tab)
* Always quote attributes
* Always use double quotes, never single quotes
* Don't include a trailing slash in self-closing elements

**Incorrect example:**

````html
<!DOCTYPE html>
<html>
<head>
<title>Page title</title>
</head>
<body>
<img src='images/company-logo.png' alt=Company />
<h1 class='hello-world'>Hello, world!</h1>
</body>
</html>
````

**Correct example:**

````html
<!DOCTYPE html>
<html>
    <head>
        <title>Page title</title>
    </head>
    <body>
        <img src="images/company-logo.png" alt="Company">
        <h1 class="hello-world">Hello, world!</h1>
    </body>
</html>
````


### HTML5 doctype

Enforce standards mode in every browser possible with this simple doctype at the beginning of every HTML page.

````html
<!DOCTYPE html>
````


### Pragmatism over semantics

Strive to maintain HTML standards and semantics, but don't sacrifice pragmatism. Use the least amount of markup with the fewest intricacies whenever possible.


### Attribute order

HTML attributes should come in this particular order for easier reading of code.

* class
* id
* data-*
* for|type|href
* checked|disabled|readonly

Such that your markup looks like:

````html
<a class="" id="" data-modal="" href="">Example link</a>
````


### Boolean attributes

Boolean HTML attributes (checked|disabled|readonly) should be set with the value the same as the attribute name.

**Incorrect example:**

````html
<button class="my-button" disabled>Click me</button>
<input type="radio" name="my-radio" checked="true">
````

**Correct example:**

````html
<button class="my-button" disabled="disabled">Click me</button>
<input type="radio" name="my-radio" checked="checked">
````


### JavaScript generated markup

Writing markup in a javascript file makes the content harder to find, harder to edit, and less performant. Don't do it.



----------



## CSS

### CSS syntax

* Use hard-tabs for indentation and spaces for alignment
* When grouping selectors, keep individual selectors to a single line
* Include one space before the opening brace of declaration blocks
* Place closing braces of declaration blocks on a new line
* Include one space after <code>:</code> in each property
* Each declaration should appear on its own line
* End all declarations with a semi-colon
* Comma-separated values should include a space after each comma
* Don't include spaces after commas in RGB or RGBa colors, and don't preface values with a leading zero
* Lowercase all hex values, e.g., <code>#fff</code> instead of <code>#FFF</code>
* Use shorthand hex values where available, e.g., <code>#fff</code> instead of <code>#ffffff</code>
* Quote attribute values in selectors, e.g., <code>input[type="text"]</code>
* Avoid specifying units for zero values, e.g., <code>margin: 0;</code> instead of <code>margin: 0px;</code>

**Incorrect example:**

````css
.selector, .selector-secondary, .selector[type=text] {
    padding:15px;
    margin:0px 0px 15px;
    background-color:rgba(0, 0, 0, 0.5);
    box-shadow:0 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}
````

**Correct example:**

````css
.selector,
.selector-secondary,
.selector[type="text"] {
    padding: 15px;
    margin: 0 0 15px;
    background-color: rgba(0,0,0,.5);
    box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
````

Questions on the terms used here? See the [syntax section of the Cascading Style Sheets article](http://en.wikipedia.org/wiki/Cascading_Style_Sheets#Syntax) on Wikipedia.


### Declaration order

Related declarations should be grouped together, placing positioning and box-model properties closest to the top, followed by typographic and visual properties.

````css
.declaration-order {
    /* Positioning */
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 100;

    /* Box-model */
    display: block;
    float: right;
    width: 100px;
    height: 100px;

    /* Visual */
    background-color: #f5f5f5;
    border: 1px solid #e5e5e5;
    border-radius: 3px;

    /* Typography */
    font: normal 13px "Helvetica Neue", sans-serif;
    line-height: 1.5;
    color: #333;
    text-align: center;

    /* Misc */
    opacity: 1;
}
````

For a complete list of properties and their order, please see [Recess](http://twitter.github.com/recess).


### Formatting exceptions

In some cases, it makes sense to deviate slightly from the default [syntax](#css-syntax).

#### Prefixed properties

When using vendor prefixed properties, indent (with spaces) each property such that the value lines up vertically for easy multi-line editing.

````css
.selector {
    -webkit-border-radius: 3px;
       -moz-border-radius: 3px;
            border-radius: 3px;
}
````

In Textmate, use **Text &rarr; Edit Each Line in Selection** (&#8963;&#8984;A).
In Sublime Text 2, use **Selection &rarr; Add Previous Line** (&#8963;&#8679;&uarr;) and **Selection &rarr;  Add Next Line** (&#8963;&#8679;&darr;).

#### Rules with single declarations

In instances where several rules are present with only one declaration each, consider removing new line breaks for readability and faster editing.

````css
.span1 { width: 60px; }
.span2 { width: 140px; }
.span3 { width: 220px; }

.sprite {
    display: inline-block;
    width: 16px;
    height: 15px;
    background-image: url(../img/sprite.png);
}
.icon           { background-position: 0 0; }
.icon-home      { background-position: 0 -20px; }
.icon-account   { background-position: 0 -40px; }
````


### Human readable

Code is written and maintained by people. Ensure your code is descriptive, well commented, and approachable by others.

#### Comments

Great code comments convey context or purpose and should not just reiterate a component or class name.

**Bad example:**

````css
/* Modal header */
.modal-header {
    ...
}
````

**Good example:**

````css
/* Wrapping element for .modal-title and .modal-close */
.modal-header {
    ...
}
````

#### Class names

* Keep classes lowercase and use dashes (not underscores or camelCase)
* Avoid arbitrary shorthand notation
* Keep classes as short and succinct as possible
* Use meaningful names; use structural or purposeful names over presentational
* Prefix classes based on the closest parent component's base class

**Bad example:**

````css
.t { ... } /* arbitrary shorthand */
.red { ... } /* presentational */
.header { ... } /* not prefixed, too generic */
````

**Good example:**

````css
.tweet { ... }
.important { ... } /* purposeful */
.tweet-header { ... } /* prefixed */
````

Some class names are acceptable

#### Selectors

* Use classes over generic element tags
* Keep them short and limit the number of elements in each selector to three
* Scope classes to the closest parent when necessary (e.g., when not using prefixed classes)

**Bad example:**

````css
span { ... }
.page-container #stream .stream-item .tweet .tweet-header .username { ... }
.avatar { ... }
````

**Good example:**

````css
.avatar { ... }
.tweet-header .username { ... }
.tweet .avatar { ... }
````

### Organization

* Organize sections of code by component
* Develop a consistent commenting hierarchy
* If using multiple CSS files, break them down by component



----------



## LESS

### File naming and directory structure

* Create a separate file for each component
* If a set of small and closely related components make sense, they can be combined into one file
* Prefix all files that are not compiled (imports) with an underscore
* Keep all mixins together in one place
* Keep variables in as few files as possible (prefer one or less for each compiled file)

### Variables and mixins

* Keep variable and mixin names lowercase and use dashes (not underscores or camelCase)
* Whan naming variables that are tied directly to HTML components, use the following order:
    * class name
    * state (hover, disabled, active, etc.)
    * css property
    * css sub-property (if applicable)

**Bad example:**

````css
@dlgWrap-shadowOnHover: #f00;
````

**Good example:**

````css
@dialog-wrapper-hover-box-shadow-color: #f00;
````

### Standard variable and mixin abbreviations

* bg - background
* xs - extra small
* sm - small
* md - medium
* lg - large
* xl - extra large



----------



## Utility suffix definitions

### Container

Use the -container suffix when an element contains one or more similar or identical children and it needs to be differentiated from the main component. Think of containers being like a `<ul>` or `<ol>` tag, where each child is the same basic type of element. Usually, the container's class should be the base class of it's children with -container appended to it. Do not simply pluralize the base class as it makes reading your stylsheets more difficult.

````html
<div class="timeline-container">
    <div class="timeline">...</div>
    <div class="timeline timeline-selected">...</div>
    <div class="timeline">...</div>
    <div class="timeline">...</div>
</div>
````

Alternately, containers can have wrappers with the same base class.

````html
<div class="timeline-container">
    <div class="timeline-wrapper">
        <div class="timeline">...</div>
        <div class="timeline-controls">...</div>
    </div>
    <div class="timeline-wrapper">...</div>
    <div class="timeline-wrapper">...</div>
</div>
</div>
````


### Wrapper

Use the -wrapper suffix when an element contains the main component element and optionally one or more different but related children. Typically, wrappers are used to help position the main component and other related elements when it doesn't make sense for the related elements to be children of the main component.

````html
<div class="timeline-wrapper">
    <div class="timeline">...</div>
    <div class="timeline-controls">...</div>
</div>
````


### Sidebar and Content

Use the -sidebar and -content suffixes when you need to have a section on the right or left such as navigation or secondary content. Use these two as a pair.

````html
<div class="foo-sidebar">
    <ul>
        <li><a href="#">Link 1</a></li>
        <li><a href="#">Link 2</a></li>
        <li><a href="#">Link 3</a></li>
    </ul>
</div>
<div class="foo-content">
    <h1>Lorem ipsum</h1>
    <p>Dolor sit amet.</p>
</div>
````


### Header, Body, and Footer

Use the -header, -body, and -footer suffixes when you need to split up content into vertically stacking sections.

````html
<header class="page-header">
    <div class="page-header-controls"></div>
</header>
<div class="page-body">
    <h1>Lorem ipsum</h1>
    <p>Dolor sit amet.</p>
</div>
<footer class="page-footer">
    <div class="page-footer-controls"></div>
</footer>
````


----------



## Copy

### Sentence case

Always write copy, including headings and code comments, in [sentence case](http://en.wikipedia.org/wiki/Letter_case#Usage). In other words, aside from titles and proper nouns, only the first word should be capitalized.



----------



### Thanks

Heavily inspired by [Idiomatic CSS](https://github.com/necolas/idiomatic-css), the [GitHub Styleguide](http://github.com/styleguide), and [Code Guide by mdo](http://github.com/mdo/code-guide).
