# css-coding-guidelines
Proposed style guide for writing CSS.  An architecture that can be followed for sustainable and maintainable CSS.

This style guide is a derivative of the following well known style guides:

* [Medium](https://medium.com/@fat/mediums-css-is-actually-pretty-fucking-good-b8e2a6c78b06)
* [SUIT CSS](https://github.com/suitcss/suit)
* [CSS Guideline](http://cssguidelin.es/)

I have taken huge pieces of each guide (shown above) and merged them into this one. I have taken
characteristics that I have personally thought will be useful in my projects.  If you find something
that you disagree with, change it and provide reasons why.

### BEM - meaning block, element, modifier
This coding guide adopts the front-end naming methodology called [BEM](https://en.bem.info/).  It is the best 
way to name your CSS classes. This will give our classes more transparency and meaning to other developers.  They
are far more strict and informative, which makes BEM naming convention ideal for teams of developers.

For this style guide we are going the change the naming for easier readability and maintainablity.

* ```Block -> component```
* ```Element -> descendant```
* ```Modifier -> modifier```

Here is the pattern:
```css
.myComponent {}
.myComponent-descendantComponent {}
.myComponent--modifier {}
```

* ```.myComponent``` represents the higher level of an abstraction or component.
* ```.myComponent-descendantComponent``` represents a descendent of ```.myComponent``` that helps form ```.myComponent``` as a whole.
* ```.myComponent--modifier``` represents a different state or version of ```.myComponent```.

For more specific examples for how to apply this naming methodology, skip to the Components section of this guide.

### NO NESTING
I know it's very tempting to go wild with selector nesting using CSS preprocessors such as LESS and SASS.  But in
this case, try to refrain from going more than 3 deep.  Keep nesting to a minimum!  Nesting Selectors is not
performant for the browser and it is a maintainability nightmare.

```css
/* bad */
.media {
  padding: 1em;
  margin: 0.5em;
  &:hover {
    background: rgba(0,0,0,0.3);
  }
  .media__body {
    font-size: 1em;
    line-height: 1.2;
    p {
      font-weight: 400;
      color: #454545;
      &:hover {
        color: #454545;
      }
    }
  }
}
/* good */
.media {
  padding: 1em;
  margin: 0.5em;
  &:hover {
    background: rgba(0,0,0,0.3);
  }
}
.media__body {
  font-size: 1em;
  line-height: 1.2;
  p {
    font-weight: 400;
    color: #454545;
  }
}
```

### Featured Details for coding guidelines
* ```.js``` Prefixed class names for elements being relied upon for javascript selectors.
* ```.u-``` Prefixed class name or single purpose utility classes like ```.u-underline```, ```.u-captialize```, etc.
* Introduction of meaningful hyphens and underscores to separate between component, descendant components, and modifies.
* ```.is-``` Prefixed classes for statefule class (often toggled by js) like ```.is-disabled``` or ```.is-show```.
* New CSS variable semantics: ```[block]__[element]--[component]``` or ```[componentName]__[descendantName]--[modifierName]```.
* Mixins reduced to polyfills only and prefixed with ```.m-```.


### Variables

CSS variable names should be structured as follows:
*property
*use
*component

[property]--[use]--[component]

Example
```css
@color-grayLight--highlightMenu: rgb(51, 51, 50);
```

Property is ```color``` followed by value ```grayLight``` that should be used for ```highlightMenu``` component.

## Colors
Color should live within their own LESS file ```colors.less``` and should be represented in RGB, RGBA or HEX.  

## Utilities

Utilities are meant to be purely structural and for positioning elements. Utilities can be used on any element;
multiple utilities, and other utilities that can be used alongside component classes.

Utilities purpose is to provide access to certain CSS properties and patterns that are used frequently together.

Example of some utilities:
* floats
* containing floats
* vertical alignment
* text truncation

Designating these patterns to utilities will help reduce repetition.  It will also provide consistency throughout 
the CSS markup and reduce code.  We won't have three different versions of clearfix in a project.

``` html
<div class="u-clearfix">
  <p class="u-textTruncate">{$text}</p>
  <img class="u-pullLeft" src="" alt="">
  <img class="u-pullLeft" src="" alt="">
  <img class="u-pullLeft" src="" alt="">
</div>
```

Syntax -> ```u-<utilityName>```

Utilities must use a camel case name, prefixed with a ```u``` namespace.  What follows is an example of how it can be used.

``` html
<div class="u-clearfix">
  <a class="u-pullLeft" href="#">
    <img class="u-block" src="" alt="">
  </a>
  <p class="u-sizeFill u-textBreak"></p>
</div>
```


## JavaScript Hooks

Do not bind your CSS and your JS onto the same class name in your HTML.  CSS and class names are more maintainable when
you bind your JavaScript to it's own class.  Not binding JS to their own class name will cause unnecessary havoc to the
code base.  For instance, if you use a class name for both CSS styles and JavaScript binding, refactoring the exiting 
class name will break the JS functionality. 

Prepend ```js-``` to class names. 
```html
<input  type="submit" class="btn js-btn" value="Submit" />
```

JavaScript specific  classes  should not be styled.

## Components

Following the BEM syntax described in this styleguide.
Syntax:```<componentName>[--modifier]-[descendantName]```

Component names should be constructed in camel case.  The purpose for component names are the following:
* Distinguishes between classes for the root element, descendant element and modifications.
* This will keep the specificity of selectors low.
* It helps decouple presentation semantics from document(layout) semantics.

Components will comprise well over the majority of CSS markup.  They are custom elements that enclose specific
semantics, styling, and behaviour.

### componentName at the root level
```css
.creditCard { }
```

```html
<article class="creditCard">
...
</article>
```

### componentName at the modifier level

A component modifier is a class that modifies the presentation of the base component in some form.
Modifier name should be written in camel case.  

```css
/* Core button */
.btn { /* ... */ }
/* Default button style */
.btn--default { /* ... */ }
```

```html 
<button class="btn btn--primary">...</button>
```

### componentName at the descendant level

Component descendant is a class that is attached to a descendant node of a componet. It's 
responsible for apply presentation directly to the descendant on behalf of a particular 
component. Descendant name should also be written in camel case.

```css
.newsItem {
...
}

.newsItem-header {
...
  &.newsItem-header--redTitle {
    color: red;
  }
}

.newsItem-avatar {
...
}

.newsItem-body {
}
```

```html
<article class="newsItem u-pullleft">
  <header class="newsItem-header">
    <div class="newsItem-title newsItem-title--default"></h2>
    <img class="newsItem-avatar" src="" alt="">
    ...
  </header>
  <div class="newsItem-body">
  ...
  </div>
</article>
```

For the CSS, remember to minimize the use of nesting.  Or don't nest at all.

### componentName at the is-stateOfComponent level

Use ```is-stateName``` for state-based modifications of components.  The state name must be
in camel case. Never style these classes.  They only should be used as adjoining classes.

JS can add/remove these classes.  You can use state name classes in multiple contexts. But
every component must define its own style for the state. 

```css
.profile { /* ... */ }
.profile.is-expanded { /* ... */ }
```

```html
<article class="profile is-expanded">
...
</article>
```

### z-Index Scale

Let's use a sensible z-index scale.  Please do not use 9999!  

Just use the z-index scale that is found in z-index.less.
```@zIndex-1 - @zIndex9``` are provided.  Nothing should be higher than ```@zIndex-9```.

### Font Weight

Raw font weights should be avoided.  Use the appropriate mixin ```.I7, .N7, etc ```

The suffix definition:

```
N = normal
I = italic
1 = ultra light weight
2 = light font-weight
3 = book font-weight
4 = normal font-weight
7 = bold font-weight
```

Refer to typography.less for type size, letter-spacing and line heights. Raw sizes, spaces, and
line heights should be avoided outside of type.less

All font sizes will be expressed in ems.  To provide a helpful guide for pixel to em translation, 
all font size variables are expressed in pixels.

```16px is 1em```

```css
@font-size-9: 0.563;
@font-size-10: 0.635em;
@font-size-11: 0.688em;
@font-size-12: 0.750em;
@font-size-13: 0.813em;
@font-size-14: 0.875em;
@font-size-15: 0.938em;
@font-size-16: 1.000em;
@font-size-17: 1.063em;
@font-size-18: 1.125em;
@font-size-20: 1.250em;
@font-size-21: 1.313em;
@font-size-22: 1.375em;
@font-size-23: 1.438em;
@font-size-24: 1.500em;
@font-size-26: 1.625em;
@font-size-28: 1.750em;
@font-size-30: 1.875em;
@font-size-31: 1.938em;
@font-size-33: 2.063em;
@font-size-32: 2em;
@font-size-34: 2.125em;
@font-size-36: 2.3em;
@font-size-40: 2.5em;
@font-size-44: 2.750em;
@font-size-48: 3em;
@font-size-60: 3.750em;
@font-size-64: 4em;
@font-size-75: 4.688em;
```

If you need a body of text to be ```18px```, just use the less variable ```@font-size-18```.  This variable will use the 
equivalent ems value of ```1.125em```.  This is very convenient since the majority of us still view sizes as pixels.

### Line Height

Please use this scale for blocks of text
```css
@lineHeight-tightest
@lineHeight-tighter
@lineHeight-tight
@lineHeight-baseSans
@lineHeight-base
@lineHeight-loose
@lineHeight-looser
```

### Letter Spacing

Please use the following scale for var scale

```css
@letterSpacing-tightest
@letterSpacing-tighter
@letterSpacing-tight
@letterSpacing-normal
@letterSpacing-loose
@letterSpacing-looser
```




