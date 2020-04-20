CSS Guidelines
========================

## Overview

We have been using SCSS as a pre-processor for the last 5 years but now we have moved to [POSTCSS](http://postcss.org/) postprocessor which has more powerfull and efficient than SCSS. Also PostCSS lets you add PostCSS plugins that enable you to manipulate your CSS in different ways.

Here is the [great article on SmashingMagazine's](https://www.smashingmagazine.com/2015/12/introduction-to-postcss/) which would help you know more about it. 


Plan your CSS
------------------------------------------------

`Before diving in and writing huge chunks of CSS, plan your styles carefully. What general styles are going to be needed, what different layouts do you need to create, what specific overrides need to be created, and are they reusable? Above all, you need to try to avoid too much overriding. If you keep finding yourself writing styles and then cancelling them again a few rulesets down, you probably need to rethink your strategy.` - Mozilla




Principles
------------------------------------------------

List of our css principles which makes our stylesheet more efficient, maintainable and scalable.

- Modular/Component based stylesheet
- Single responsibility selectors
- Separation of structure from skin OOCSS
- Separation of containers and content OOCSS
- Low CSS specificity
- Low to high specificity stylesheet ITCSS

Terminology
------------------------------------------------

Concise terminology used in these standards:

    selector {
    property: value;
    }

property: value makes a declaration. Selector and declarations makes a rule.

Write Valid Css
------------------------------------------------

Use valid CSS where possible.

Unless dealing with CSS validator bugs or requiring proprietary syntax, use valid CSS code.

Use tools such as the [W3C CSS validator](https://jigsaw.w3.org/css-validator/) to test.

Using valid CSS is a measurable baseline quality attribute that allows to spot CSS code that may not have any effect and can be removed, and that ensures proper CSS usage.

Don't use resets
------------------------------------------------

For maximum control over CSS across platforms, a lot of people used to use CSS resets to remove every style, before then building things back up themselves. This certainly has its merits, but especially in the modern world CSS resets can be overkill, resulting in lots of extra time spent reimplementing things that weren't completely broken in the first place, like default margins, list styles, etc.

If you really feel like you need to use a reset, consider using [normalize.css by Nicolas Gallagher](http://necolas.github.io/normalize.css/), which aims to just make things more consistent across browsers, get rid of some default annoyances that we always remove (the margins on `<body>`, for example) and fix a few bugs.

CSS Hacks
------------------------------------------------

Avoid user agent detection as well as CSS “hacks”—try a different approach first.

It’s tempting to address styling differences over user agent detection or special CSS filters, workarounds, and hacks. Both approaches should be considered last resort in order to achieve and maintain an efficient and manageable code base. Put another way, giving detection and hacks a free pass will hurt projects in the long run as projects tend to take the way of least resistance. That is, allowing and making it easy to use detection and hacks means using detection and hacks more frequently—and more frequently is too frequently.

CSS Quotation Marks
------------------------------------------------

Use single (`''`) rather than double (`""`) quotation marks for attribute selectors and property values.

Do not use quotation marks in URI values (`url()`).

Exception: If you do need to use the `@charset` rule, use double quotation marks—[single quotation marks are not permitted](https://www.w3.org/TR/CSS21/syndata.html#charset).

Media Queries
------------------------------------------------

**Mobile First**

When including different sets of styles for different target viewport sizes using media queries inside the same stylesheet, it is a good idea to make the default styling before any media queries have been applied to the document the narrow screen/mobile styling, and then override this for wider viewports inside successive media queries.

```css
/*Default CSS layout for narrow screens*/

@media (min-width: 480px) {
  /*CSS for medium width screens*/
}

@media (min-width: 800px) {
  /*CSS for wide screens*/
}

@media (min-width: 1100px) {
  /*CSS for really wide screens*/
```

Comments
------------------------------------------------

Group sections by a section comment (optional).

If possible, group style sheet sections together by using comments. Separate sections with new lines.

```css 
/* ==========================================================================
   Header
   ========================================================================== */

#adw-header {}

/* Footer
   ========================================================================== */

#adw-footer {}

// Gallery 

.adw-gallery {}
```

This comment style is used as the separator of the main sections. There are 2 empty lines before and after it:

```css
/* ==========================================================================
   Section comment block
   ========================================================================== */
```

The following comment style is used as the separator of the subsections of the main sections. It has 2 empty lines before it and 1 empty line after it:

```css
/* Sub-section comment block
   ========================================================================== */
```
Use single-line comments `// comment` instead of multi-line comments `/* comment */`. This lets you span legitimate comments with code you’d like to temporarily cancel out.

This comment style is used for commenting particular page elements. It has 1 empty line before it and no empty lines after it (it is immediately followed by the rules):

```css
// Pager 
.pager {
  padding-bottom: 5px;
  border-bottom: 1px solid #ccc;
}
```

Properties
------------------------------------------------
Every declaration should be on its own line below the opening brace. Each property should:

- have a single sof tab with 2 spaces before the property name and a single space before the property value.
- end in a semi-colon.

```css
.site-name span {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 10;
}
```
Use shorthand properties where possible.

CSS offers a variety of [shorthand](https://www.w3.org/TR/CSS21/about.html#shorthand) properties (like `font`) that should be used whenever possible, even in cases where only one value is explicitly set.

Using shorthand properties is useful for code efficiency and understandability.

```css 
/* Not recommended */
border-top-style: none;
font-family: palatino, georgia, serif;
font-size: 100%;
line-height: 1.6;
padding-bottom: 2em;
padding-left: 1em;
padding-right: 1em;
padding-top: 0;
```

```css 
/* Recommended */
border-top: 0;
font: 100%/1.6 palatino, georgia, serif;
padding: 0 1em 2em;
```

Use a space after a property name’s colon.

Always use a single space between property and value (but no space between property and colon) for consistency reasons.

```css 
/* Not recommended */
h3 {
  font-weight:bold;
}
```

```css 
/* Recommended */
h3 {
  font-weight: bold;
}
```

Declaration Order
------------------------------------------------

**Basic**

Related property declarations should be grouped together following the order:

1. Positioning
2. Box model
3. Typographic
4. Visual

Positioning comes first because it can remove an element from the normal flow of the document and override box model related styles. The box model comes next as it dictates a component's dimensions and placement.

Everything else takes place inside the component or without impacting the previous two sections, and thus they come last.

```css
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

  /* Typography */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;

  /* Visual */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* Misc */
  opacity: 1;
}
```


**Preprocessor**

- Limit nesting to 1 level deep. Reassess any nesting more than 2 levels deep. This prevents overly-specific CSS selectors.

- Avoid large numbers of nested rules. Break them up when readability starts to be affected. Preference to avoid nesting that spreads over more than 20 lines.

- Always place `@extend` statements on the first lines of a declaration block.

- Where possible, group `@include` statements at the top of a declaration block, after any `@extend` statements.

```css
.selector-1 {
  @extend .other-rule;
  @include clearfix();
  @include box-sizing(border-box);

  margin: 10px;
  padding: 10px;
}
```

Selectors
------------------------------------------------

**Type Selectors**

Avoid qualifying ID and class names with type selectors.

Unless necessary (for example with helper classes), do not use element names in conjunction with IDs or classes.

Avoiding unnecessary ancestor selectors is useful for [performance reasons](http://www.stevesouders.com/blog/2009/06/18/simplifying-css-selectors/).

```css
/* Not recommended */
ul#example {}
div.error {}
```

```css
/* Recommended */
#example {}
.error {}
```

**Complex Selectors**

Avoid very complex child and descendant selectors like:

```css
/* Not recommended */
.my-inbox .flyout-content .inner .message .inbox li div.take-action .actions ul li a {
}
```

**Multiple Selectors**

Multiple selectors should each be on a single line, with no space after each comma.

```css
.faqs a.open,
.faqs a.close {
}
```

**Prefixes**

Prefix selectors with an application-specific prefix (optional).

In large projects as well as for code that gets embedded in other projects or on external sites use prefixes (as namespaces) for ID and class names. Use short, unique identifiers followed by a dash.

Using namespaces helps preventing naming conflicts and can make maintenance easier, for example in search and replace operations.

```css
.adw-help {} /* AdWords */
#maia-note {} /* Maia */
```


ID and Classnames
------------------------------------------------

**Naming:**

Use meaningful or generic ID and class names.

Instead of presentational or cryptic names, always use ID and class names that reflect the purpose of the element in question, or that are otherwise generic.

Names that are specific and reflect the purpose of the element should be preferred as these are most understandable and the least likely to change.

Generic names are simply a fallback for elements that have no particular or no meaning different from their siblings. They are typically needed as “helpers.”

Using functional or generic names reduces the probability of unnecessary document or template changes.

```css
/* WRONG */

/* Not recommended: meaningless */
#yee-1901 {}

/* Not recommended: presentational */
.button-green {}
.clear {}
```

```css
/* RIGHT */

/* Recommended: specific */
#gallery {}
#login {}
.video {}

/* Recommended: generic */
.aux {}
.alt {}
```

**Style:**

Use ID and class names that are as short as possible but as long as necessary.

Try to convey what an ID or class is about while being as brief as possible.

Using ID and class names this way contributes to acceptable levels of understandability and code efficiency.

```css
/* WRONG */

/* Not recommended */
#navigation {}
.atr {}
```
```css
/* RIGHT */

/* Recommended */
#nav {}
.author {}
```


Naming Conventions
------------------------------------------------

These are the methodologies we use to stick on our css principles projects.

- [BEM](http://getbem.com/) - We use this for naming convention. Read [documentation](https://en.bem.info/methodology/naming-convention/)
- [ITCSS](itcss.io) - We use this for organize our css files. Read [documentation](http://www.hongkiat.com/blog/inverted-triangle-css-web-development/)
- [OOCSS](oocss.org) - We use its two Principles. Read [documentation](https://appendto.com/2014/04/oocss/)

**BEM - Block Element Modifier**: is a popular naming convention for classes in CSS. Its goal is to help developers better understand the relationship between the Components, Also prevent extra selector nesting.

[Here is article which can help you understand more.](https://css-tricks.com/bem-101/)

**Example:**

```css
/* RIGHT */

/* Component */
.c-hero {}

/* Child of the Component */ 
.c-hero__head {}
.c-hero__subHead {}

/* Modifier that changes the style of the component */
.c-hero--wide {} 

```
```css

/* WRONG */

/* Component */
.c-hero {}

/* Child of the Component */ 
.c-hero__head {}
.c-hero__head__icon {}
.c-hero__head__icon__small {}

/* Modifier that changes the style of the component */
.c-hero--wide {} 
```


**ITCSS - Inverted Triangle CSS**: it helps us to organize your project CSS files in such way that we can better deal with CSS specifics like global namespace, cascade and selectors specificity. One of the key principles of ITCSS is that it separates the CSS codebase to several sections (called layers), which take form of the inverted triangle:

- **Settings** – Used with postprocessors and contain `font`, `colors` `definitions`, etc.

- **Tools** – Globally used mixins and functions. It’s important not to output any CSS in the first 2 layers.

- **Generic** – reset and/or normalize styles, box-sizing definition, etc. This is the first layer which generates actual CSS.

- **Elements** – styling for bare HTML elements (like `H1`, `A`, etc.). These come with default styling from the browser so we can redefine them here.

- **Objects** – class-based selectors which define undecorated design patterns, for example media object known from OOCSS.

- **Components** – specific UI components. This is where majority of our work takes place and our UI components are often composed of Objects and Components

- **Trumps** - utilities and helper classes.

**OOCSS - Object oriented CSS** : is a methodology of writing reusable CSS that is fast, scalable and maintainable.

Syntax and formatting
------------------------------------------------

- Use multi-line CSS declarations. This helps with version control (diff-ing single line CSS can be a nightmare). Group CSS declarations by type - keeping font related styling together, layout styling together etc - and ordered by relevance, not alphabetized.
- All CSS rules should have a space after the selector colon and a trailing semi-colon.
- Selectors should be specified using of BEM.
- use camel-casing if more than one word: e.g. twoWords.
- use double underscore for child of component. 
- use double hyphen for Modifier of the component.
- selector names should be semantic instead of presentational.

**Example**

```css
/* use camel-casing if more than one word: e.g. twoWords */
.o-oneColumnGrid {
    ...
}

/* ========= */

/* Child elements use double underscore: __ */
.c-nav__link {
    ...
}

/* ========= */

/* Modifier component use a double hyphen: -- */
.btn--small {
    ...
}

/* ========= */

/* Semantic/

.c-btn__primary {
    ...
}

/* ========= */

Presentational

.c-btn__red {
    ...
}
```

Indentation
------------------------------------------------

For all languages, indent your code with tabs. The default tab size should be set as 4.

When indenting Sass or PostCSS, stick to the same four (4) spaces, and also leave a blank line before and after the nested ruleset.

**Example:**

```css
.c-nav {
    color: red;
}

    .c-nav__link {
    color: red;
    }
```


Component and Object Organization
------------------------------------------------

- Organize sections of code by component or object in the correct order provided by ITCSS
- Develop a consistent commenting hierarchy. As I mentioned in CSS Methodology section.
- Skin should be different from layout as per OOCSS principle.
- When using multiple CSS files, break them down by component instead of page. Pages can be rearranged and components moved.

```css 
/* Component */
.c-hero {}

/* Child of the Component */ 
.c-hero__head {}
.c-hero__subHead {}

/* Modifier that changes the style of the Component */
.c-hero--wide {} 
```



Values
------------------------------------------------

Always define generic font families like sans-serif or serif.

```css 
/* Correct */
font-family: "ff-din-web-1", Arial, Helvetica, sans-serif;

/* Wrong */
font-family: "ff-din-web-1";
```

Use 3 character hexadecimal notation where possible.

For color values that permit it, 3 character hexadecimal notation is shorter and more succinct.

```css 
background: #fff;
```

Omit unit specification after “0” values, unless required.

Do not use units after 0 values unless they are required.

```css 
flex: 0px; /* This flex-basis component requires a unit. */
flex: 1 1 0px; /* Not ambiguous without the unit, but needed in IE11. */
margin: 0;
padding: 0;
```

Omit leading “0”s in values.

Do not put 0s in front of values or lengths between -1 and 1.

```css 
font-size: .8em;
```

Do not use default values if they are not necessary to override inherited values.

