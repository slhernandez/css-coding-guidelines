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

Here is the pattern:
```css
.block {}
.block__element {}
.block--modifier {}
```

* ```.block``` represents the higher level of an abstraction or component.
* ```.block__element``` represents a descendent of ```.block``` that helps form ```.block``` as a whole.
* ```.block--modifier``` represents a different state or version of ```.block```.

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





