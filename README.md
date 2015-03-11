# css-coding-guidelines
Proposed style guide for writing CSS.  An architecture that can be followed for sustainable and maintainable CSS.

## Featured Details for coding guidelines
* ```.js``` Prefixed class names for elements being relied upon for javascript selectors.
* ```.u-``` Prefixed class name or single purpose utility classes like ```.u-underline```, ```.u-captialize```, etc.
* Introduction of meaningful hyphens and underscores to separate between component, descendant components, and modifies.
* ```.is-``` Prefixed classes for statefule class (often toggled by js) like ```.is-disabled``` or ```.is-show```.
* New CSS variable semantics: ```[block]__[element]--[component]``` or ```[componentName]__[descendantName]--[modifierName]```.
* Mixins reduced to polyfills only and prefixed with ```.m-```.


## Variables

CSS variable names should be structured as follows:
*property
*use
*component

```[property]--[use]--[component]s```

Example
```css
@color-grayLight--highlightMenu: rgb(51, 51, 50);
```

Property is ```color``` followed by value ```grayLight``` that should be used for ```highlightMenu``` component.

## Colors
Color should live within their own LESS file ```colors.less``` and should be represented in RGB, RGBA or HEX.  






