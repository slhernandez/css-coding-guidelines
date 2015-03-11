# css-coding-guidelines
Proposed style guide for writing CSS.  An architecture that can be followed for sustainable and maintainable CSS.

## Featured Details for coding guidelines
* ```.js``` Prefixed class names for elements being relied upon for javascript selectors.
* ```.u-``` Prefixed class name or single purpose utility classes like ```.u-underline```, ```.u-captialize```, etc.
* Introduction of meaningful hyphens or underscores to separate between component, descendant components, and modifies.
* ```.is-``` Prefixed classes for statefule class (often toggled by js) like ```.is-disabled``` or ```.is-show```.
* New CSS variable semantics: [property]__[value]--[component]
* Mixins reduced to polyfills only and prefixed with ```.m-```.


