# CSS
*An opinionated guide*

## Table of Contents

  1. [Functional CSS](#functional-css)
  1. [Cascading](#cascading)
  1. [Style only classes](#style-only-classes)
  1. [Keep css easy to read](#keep-css-easy-to-read)
  1. [Keep breakpoints within their class](#keep-breakpoints-within-their-class)

----

## Functional CSS
- [2](#functional-css) While it's great for quickly building pages, it starts to get in the way when building something more complex and custom.

#### PRO
- Simple to use for people unfamiliar with CSS
- Good documentation
- Small amount of CSS
- Attractive designs (using https://tachyons.io)

#### CONS
- Custom components that can’t be styled by the classes provided
- When using breakpoints need a long list of classes overriding each other
- Styling is happening in HTML, rather then in CSS, where it is instead supposed to happen


```html
// bad
// tachyons
<h4 class="mt4 fw6 f6">Narrow Measure</h4>

// bad
// tailwind
<button class="text-xs font-semibold rounded-full px-4 py-1 leading-normal bg-white border border-purple text-purple hover:bg-purple hover:text-white">Message</button>

// good
// SUIT
<h1 class="Component-heading">Hello</h1>
```

```css
// good
// SUIT
.Component-heading {
  font-size: 12px;
  color: blue;
  letter-spacing: 0.2px;
  font-weight: 500;
  line-height: 1.5;
}
```

```html
// future?
// using robots
<div id="tophf"></div>
```

----

## Cascading
- [2](#cascading) CSS (Cascading Style Sheet) becomes easier when you STOP using cascading.

> Why? Think separation of concerns, single responsability principle, loose coupling. Build a whole bunch of tiny little CSS modules that:
  - Can't know about the other ones near them
  - Need to be able to operate on their own
  - Can't be too dependent on what's above them or below them

** Add visual example here of visual margin difference on headline and color blocks **

```html
// bad
<h1 class="Banner-margin"></h1>
<img class="Banner-margin">
<button class="Banner-margin"></button>
```
```css
.Banner-margin {
  margin-bottom: 12px;
}
```

```html
// good
<h1 class="Banner-heading"></h1>
<img class="Banner-picture">
<button class="Banner-button"></button>
```
```css
.Banner-heading {
  margin-bottom: 12px;
}

.Banner-picture {
  margin-bottom: 16px;
}

.Banner-button {
  margin-bottom: 24px;
}
```

----

## Style only classes

- [3](#style-only-classes) Style only classes and use SUIT classname convention.

> Why? Styling element bumps the specificity of a style. It's very easy to think there will only be one <button> inside .Banner, until soon after you'll need to add one more and overriding styling will be much more complicate.

```html
// bad
// styling element
<div class="Banner">
  <button></button>
  <button class="OtherButton"></button>
</div>
```
```css
// bad
// styling element
.Banner button {
  height: 24px; // higher specificity
}

.Banner .OtherButton {
  height: 16px;
}
```

```html
// good
// styling classes
<div class="Banner">
  <button class="Banner-buttonPrimary"></button>
  <button class="Banner-buttonSecondary"></button>
</div>
```
```css
// good
.Banner-buttonPrimary {
  height: 24px;
}

.Banner-buttonSecondary {
  height: 16px;
}
```

----

## Keep CSS easy to read

- [4](#keep-css-easy-to-read)

> Why? CSS property are very descriptive and easy to read. Abusing of mixins and functions makes less intuitive to understand the styling. Short acronyms are difficult to decipher as well.

```css
// bad
.mfn {
  margin-bottom: 24px;
}

// bad
$button-padding-bottom: 16px;

.Button {
  padding-bottom: $button-padding-bottom;
}

// bad
@mixin button-padding($size, $color) {
  font-size: $size;
  color: $color;
}

.Button {
  @include button-padding(16px, red);
}

// good
.Button {
  font-size: 16px;
  color: red;
}
```

----

## Breakpoints

- [5.1](#breakpoints--keep-within-their-class) Group breakpoints inside each class. Don't put them at the end of the page, or even worse in a different file.

> Why? It is clearer to see how each class changes between resolution when they're grouped together by classname.

```css
// terrible
// scss/homepage/_breakpoints.scss

@media screen and (min-width 768px) {

  .Button {
    height: 24px;
  }

  .Heading {
    font-size: 32px;
  }
}
```


```css
// bad
// scss/_component.scss

.Button {
  height: 12px;
}

.Heading {
  font-size: 24px;
}

.Image {
  width: 50%;
}

@media screen and (min-width 768px) {

  .Button {
    height: 14px;
  }

  .Heading {
    font-size: 28px;
  }

  .Image {
    width: 75%;
  }
}

@media screen and (min-width 1200px) {

  .Button {
    height: 16px;
  }

  .Heading {
    font-size: 32px;
  }

  .Image {
    width: 80%;
  }
}
```

```css
// good

.Button {
  height: 12px;

  @media (min-width 768px) {
    height: 14px;
  }

  @media (min-width 1200px) {
    height: 16px;
  }
}

.Heading {
  font-size: 24px;

  @media (min-width 768px) {
    height: 28px;
  }

  @media (min-width 1200px) {
    height: 32px;
  }
}
```

- [5.2](#breakpoints--use-only-one-direction) Use only min-width, one direction from smaller screen size to larger.

> Why? Ideally we desing `mobile first`. Also, traditionally screen resolutions are getting larger, rather then the opposite.

```css
// bad

.Button {
  height: 16px;

  @media (max-width 1200px) {
    height: 14px;
  }

  @media (max-width 768px) {
    height: 12px;
  }
}
```

```css
// good

.Button {
  height: 12px;

  @media (min-width 768px) {
    height: 14px;
  }

  @media (min-width 1200px) {
    height: 16px;
  }
}
```

----

## Margins and Paddings

- [6.1](#margins--go-one-direction) Use only one direction, downwards.

> Why? It is very confusing when a margin bottom and a following margin bottom blend into each other.

```css
// bad

.Image {
  margin-bottom: 32px;
}

.Caption {
  margin-top: 8px;
  margin-bottom: 4px;
}

.Time {
  ...
}
```

```css
// good

.Image {
  margin-bottom: 32px;
}

.Caption {
  margin-bottom: 4px;
}
```

- [6.2](#margins--padding) Use mostly paddings.

> Why? They don't interfere with each other.


- [6.3](#margins--put-margin-to-parent-wrapper) Keep components without margin. Add wrapper elements on case by case for margins.

```html
// bad
<div class="Homepage">
  {{bsk-button}}
  {{bsk-button}}
</div>

<div class="Homepage">
  {{bsk-button class='bsk-Button--noMargin'}}
  <i>icon</i>
</div>

//
```
```css
// bad
.Homepage .bsk-Button {
  margin-right: 8px;
}

.bsk-Button--noMargin {
  margin-right: 0;
}
```

```html
// good
<ul class="Homepage-buttons">
  <li class="Homepage-button">
    {{bsk-button}}
  </li>
  <li class="Homepage-button">
    {{bsk-button}}
  </li>
</div>

<div class="Homepage-buttons">
  <div class="Homepage-button">
    {{bsk-button}}
  </div>
  <i class="bsk-icon-form"></i>
</div>
//
```
```css
.Homepage-button {
  margin-right: 8px;
}
```

----

## Component, not pages

- [7.1](#component) Everything is a component. Create small readable components.

- [7.2](#component) If a component can display content in two different ways, then sounds to me they are different enough to be two different components. Keep component small, doing one thing only. Easier to debug. Easier to visualize.

----

## Animation

- [8.0](#animation--guideline). Should be fast, snappy, sometimes almost invisible.
- In experience, give a feedback to a button pushed, signify what's happening or something point the user to something they should be paying attention to (scroll down arrow on better.com).
- In data visualization, to simplify transition.
- Stick to `transform` and `opacity` if possible, which are the ones GPU optimized

- [8.1](#animation--bezier) Use our custom bezier curve rather then simple ease-in-out. Feels more organic. Less regular.

- [8.2](#animation--faster-slower) Animate hover faster, otherwise the element feel 'slow' to react. Power users will like something that feels snappy and quick. On hover out, the animation can be slower.
Button: https://jsbin.com/pobobol/edit?html,css,output
Toggle: https://jsbin.com/bakover/edit?html,css,output
Card: https://jsbin.com/qikuruq/edit?html,css,output

----

## Typography

- [8.1](#typograhy--scale) Type scale, line-height, font-weight, letter-spacing.

Scale: https://jsfiddle.net/gvocale/Lsdcotq5/19/

----

## Data attribute

- [8.1](#data-attribute)

Example: https://jsfiddle.net/gvocale/pcwudrmc/70450/
