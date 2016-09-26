AnattaDesign frontend development guidelines
========================

## Overview

This document details the guidelines and standards adhered to by the AnattaDesign, Inc., and all web applications built should take these into consideration.  It is an evolving document and should be reviewed as and when required to keep up with changes in technology and best practice.

- [General Guidelines](#gg)
- [Markup Guidelines](#mg)
- [CSS Guidelines and best practice](#cg)
- [JavaScript Guidelines](#jg)
- [Speed Optimization Guidelines](#og)
- [Build Tool](#bt)

## Purpose

Our motivations in creating this document are to:

- Maintain code quality and consistency on accross the projects. 
- More optimized and efficient CSS code.
- Predictable, reusable, maintainable, and scalable stylesheets.
- Ensure we create professional quality Web sites.
- Guide staff on-boarding or educate new developers.  

<a name="gg"></a>Notes you need to consider before starting coding
------------------------------------------------

- Review design/styleguide carefully, if you did not find any styleguide in design files ask our design team to create one.
- Come up with list of common componenets and objects which would be used multipule times in application. like `buttons`, `navigations`and `forms` etc.
- Update styleguide variables in our library.
- Modify the grid by modifying its variables, if required.
- List out the javascript functionality and libraries.
- Have discussion with team leader and put schedule together on basecamp.
- Setup staging server.
- Setup depoyment system.
- Now get started with building common components and styleguide.


Browser Support
------------------------------------------------

- Internet Explorer 9+
- Firefox 
- Google Chrome
- Safari
- Opera 

They might vary based on projects.

Base Templates and frameworks
------------------------------------------------

Due to some valid reasons, we have decided to not use Bootstrap and Foundation or any other, so we have created our own UI library and frontend architecture by following best practices. You can learn more [here](http://google.com)

Compression
------------------------------------------------

We use server-side or build processes to automatically minify and gzip all static client-side files, such as CSS and JavaScript.

Grid System
------------------------------------------------

We use [lost](https://github.com/peterramsing/lost) grid system and its already included in your library.

<a name="mg"></a>Markup Guidelines
========================

We use HTML5 and do not use preprocessor(such as HAML, Jade, etc)? 

To ensure HTML5 markup compatibility with older browsers, use either:

- [Modernizr](https://modernizr.com/) - consider bloat, use the build generator to decrease its size
- [HTML5shiv](https://github.com/afarkas/html5shiv) - no feature detection, simply ensures markup compatibility

We will test our markup against the [W3C validator](http://validator.w3.org/), to ensure that the markup is well formed. 100% valid code is not a goal, but validation certainly helps to write more maintainable sites as well as debugging code. TMW does not guarantee markup is 100% valid, but instead assures the cross-browser experience is consistent.

General
------------------------------------------------
The following are general guidelines for structuring your HTML markup. Authors are reminded to always use markup which represents the semantics of the content in the document being created.

- Use `<p>` elements for paragraph delimiters as opposed to multiple `<br />` tags.
- Items in list form should always be housed in a `<ul>`, `<ol>`, or `<dl>`, never a set of `<div>`s or `<p>`s.
- Make use of `<thead>`, `<tbody>`, and `<th>` tags (and Scope attribute) when appropriate.
- Make use of `<dl>` (definition lists) and `<blockquote>`, when appropriate.
- Use `<label>` fields to label each form field. The for attribute should associate itself with the input field, so users can click the labels and obtain focus.
- Do not use the `size` attribute on your input fields. The `size` attribute is relative to the `font-size` of the text inside the input. Instead use CSS width.
- Tables shouldn't ever be used for page layout – only for tabular data.

Syntax
------------------------------------------------

- Use tabs instead of spaces for markup indentation.
- Nested elements should be indented once (two spaces).
- Always use double quotes, never single quotes, on attributes.
- Don't include a trailing slash in self-closing elements—the HTML5 spec says they're optional.
- Don’t omit optional closing tags (e.g. `</li>` or `</body>`).

**Example:**


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



HTML5 doctype
------------------------------------------------

Enforce standards mode and more consistent rendering in every browser possible with this simple doctype at the beginning of every HTML page.

**Example:**

	<!DOCTYPE html>
	<html>
		<head>
		</head>
	</html>	

IE compatibility mode
------------------------------------------------

Internet Explorer supports the use of a document compatibility `<meta>` tag to specify what version of IE the page should be rendered as. Unless circumstances require otherwise, it's most useful to instruct IE to use the latest supported mode with edge mode.

For more information, [read this awesome Stack Overflow article.](http://stackoverflow.com/questions/6771258/what-does-meta-http-equiv-x-ua-compatible-content-ie-edge-do)

Character encoding
------------------------------------------------

Quickly and easily ensure proper rendering of your content by declaring an explicit character encoding. When doing so, you may avoid using character entities in your HTML, provided their encoding matches that of the document (generally UTF-8).

**Example:**

	<head>
		<meta charset="UTF-8">
	</head>

CSS and JavaScript includes
------------------------------------------------

Per HTML5 spec, typically there is no need to specify a `type` when including CSS and JavaScript files as `text/css` and `text/javascript` are their respective defaults.

**Example:**

	<!-- External CSS -->
	<link rel="stylesheet" href="app.css">

	<!-- In-document CSS -->
	<style>
	  /* ... */
	</style>

	<!-- JavaScript -->
	<script src="app.js"></script>

Attribute order
------------------------------------------------

HTML attributes should come in this particular order for easier reading of code.

- `class`
- `id`, `name`
- `data-*`
- `src`, `for`, `type`, `href`, `value`
- `title`, `alt`
- `role`, `aria-*`

**Example:**

	<a class="..." id="..." data-toggle="modal" href="#">
	  Example link
	</a>

	<input class="form-control" type="text">
	<img src="..." alt="...">

Reducing markup
------------------------------------------------

Whenever possible, avoid superfluous parent elements when writing HTML. Many times this requires iteration and refactoring, but produces less HTML.

**Example:**

	<!-- Not so great -->
	<span class="c-avatar">
		<img src="...">
	</span>

	<!-- Better -->
	<img class="c-avatar" src="...">

JavaScript generated markup
------------------------------------------------

Writing markup in a JavaScript file makes the content harder to find, harder to edit, and less performant. Avoid it whenever possible.

Markup comments
------------------------------------------------

Avoid using HTML comments. 

	<!-- I don't need to be here -->
	<p>Lorem ipsum dolor sit amet.</p>

 Why not?

- With modern developer tools, the need to “View Source” is rare today.
- Developer annotations should be secret (HTML comments are not).
- Save users from downloading useless bytes.


<a name="cg"></a>CSS Guidelines
========================

We were using SCSS as a pre-processor from last 2 years but now we have moved to [POSTCSS](http://postcss.org/) postprocessor which more powerfull and efficient than SCSS. Also PostCSS lets you add PostCSS plugins that enable you to manipulate your CSS in different ways.

Here is the [great article on SmashingMagazine's](https://www.smashingmagazine.com/2015/12/introduction-to-postcss/) which would help you know more about it. 


Principles
------------------------------------------------

List of our css principles which makes our stylesheet more efficient, maintainable and scalable.

- Modular/Component based stylesheet
- Single responsibility selectors
- Separation of structure from skin [OOCSS](http://oocss.org/)
- Separation of containers and content [OOCSS](http://oocss.org/)
- Low CSS specificity
- Low to high specificity stylesheet [ITCSS](https://www.xfive.co/blog/itcss-scalable-maintainable-css-architecture/)
	

CSS Methodology
------------------------------------------------

These are the methodology which use to stick on our css principles to across the projects.

- [BEM](http://getbem.com/) - We use this for naming convention. Read [documentation](https://en.bem.info/methodology/naming-convention/)
- [ITCSS](itcss.io) - We use this for organize our css files. Read [documentation](http://www.hongkiat.com/blog/inverted-triangle-css-web-development/)
- [OOCSS](oocss.org) - We use its two Principles. Read [documentation](https://appendto.com/2014/04/oocss/)

**BEM - Block Element Modifier**: is a popular naming convention for classes in CSS. Its goal is to help developers better understand the relationship between the Components, Also prevent extra selector nesting.

[Here is article which can help you understand more.](https://css-tricks.com/bem-101/)

**Example**

	Good method:

	/* Component */
	.c-hero {}

	/* Child of the Component */ 
	.c-hero__head {}
	.c-hero__subHead {}

	/* Modifier that changes the style of the component */
	.c-hero--wide {} 

	Bad method:

	/* Component */
	.c-hero {}

	/* Child of the Component */ 
	.c-hero__head {}
	.c-hero__head__icon {}
	.c-hero__head__icon__small {}

	/* Modifier that changes the style of the component */
	.c-hero--wide {} 

**ITCSS - Inverted Triangle CSS**: it helps us to organize your project CSS files in such way that we can better deal with CSS specifics like global namespace, cascade and selectors specificity. One of the key principles of ITCSS is that it separates the CSS codebase to several sections (called layers), which take form of the inverted triangle:

- **Settings** – Used with postprocessors and contain `font`, `colors` `definitions`, etc.

- **Tools** – Globally used mixins and functions. It’s important not to output any CSS in the first 2 layers.

- **Generic** – reset and/or normalize styles, box-sizing definition, etc. This is the first layer which generates actual CSS.

- **Elements** – styling for bare HTML elements (like `H1`, `A`, etc.). These come with default styling from the browser so we can redefine them here.

- **Objects** – class-based selectors which define undecorated design patterns, for example media object known from OOCSS.

- **Components** – specific UI components. This is where majority of our work takes place and our UI components are often composed of Objects and Components

- **Trumps** - utilities and helper classes.

**OOCSS - Object oriented CSS** : is a methodology of writing reusable CSS that is fast, scalable and maintainable.


Namespacing
------------------------------------------------

This is taken straight from Harry Roberts' article on namespacing but We have made small modifications.

- **o-:** Signify that something is an Object, and that it may be used in any number of unrelated contexts to the one you can currently see it in. Making modifications to these types of class could potentially have knock-on effects in a lot of other unrelated places. Tread carefully.

- **c-:** Signify that something is a Component. This is a concrete, implementation-specific piece of UI. All of the changes you make to its styles should be detectable in the context you’re currently looking at. Modifying these styles should be safe and have no side effects.

- **u-:** Signify that this class is a Utility class. It has a very specific role (often providing only one declaration) and should not be bound onto or changed. It can be reused and is not tied to any specific piece of UI. You will probably recognise this namespace from libraries and methodologies like SUIT.

- **t-:** Signify that a class is responsible for adding a Theme to a view. It lets us know that UI Components’ current cosmetic appearance may be due to the presence of a theme.

- **is-, has-:** Signify that the piece of UI in question is currently styled a certain way because of a state or condition. This stateful namespace is gorgeous, and comes from SMACSS. It tells us that the DOM currently has a temporary, optional, or short-lived style applied to it due to a certain state being invoked.

- **js-:** Signify that this piece of the DOM has some behaviour acting upon it, and that JavaScript binds onto it to provide that behaviour. If you’re not a developer working with JavaScript, leave these well alone.

- **qa-:** Signify that a QA or Test Engineering team is running an automated UI Test which needs to find or bind onto these parts of the DOM. Like the JavaScript namespace, this basically just reserves hooks in the DOM for non-CSS purposes.

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


Indentation
------------------------------------------------

For all languages, indent your code with tabs. The default tab size should be set as 4.

When indenting Sass or PostCSS, stick to the same four (4) spaces, and also leave a blank line before and after the nested ruleset.

**Example:**

	.c-nav {
    	color: red;
    	
        .c-nav__link{
       		color: green;
        }
        
    }
   
 
Comment formats
------------------------------------------------   

Use single-line comments `// comment` instead of multi-line comments `/* comment */`. This lets you span legitimate comments with code you’d like to temporarily cancel out. 

Declaration order
------------------------------------------------   

Related property declarations should be grouped together following the order:

1. Positioning
2. Box model
3. Typographic
4. Visual

Positioning comes first because it can remove an element from the normal flow of the document and override box model related styles. The box model comes next as it dictates a component's dimensions and placement.

Everything else takes place inside the component or without impacting the previous two sections, and thus they come last.

**Example:**


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

Media query placement
------------------------------------------------   

Place media queries in their relevant rule sets. 


Component and Object Organization
------------------------------------------------

- Organize sections of code by component or object in the correct order provided by ITCSS
- Develop a consistent commenting hierarchy. As I mentioned in CSS Methodology section.
- Skin should be different from layout as per OOCSS principle.
- When using multiple CSS files, break them down by component instead of page. Pages can be rearranged and components moved.

**Example**

	/* Component */
	.c-hero {}

	/* Child of the Component */ 
	.c-hero__head {}
	.c-hero__subHead {}

	/* Modifier that changes the style of the Component */
	.c-hero--wide {} 


<a name="jg"></a>JavaScript Guidelines
========================

	/* Comming soon */

<a name="og"></a>Speed Optimization Guidelines
========================

	/* Comming soon */

<a name="bt"></a>Build Tools
========================

Eariler we were using [Gulp](http://gulpjs.com/) but now moved on [Webpack](https://webpack.github.io/) because it has lot more features. Webpack is a module bundler and it takes modules with dependencies and generates static assets representing those modules.

Its already integrated in our UI library so you can read the [instructions](http://google.com) there.

