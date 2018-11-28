# CSS
*An opinionated guide*

## Table of Contents

  1. [Functional CSS](#functional-css)
  1. [Cascading](#cascading)
  1. [Style only classes](#style-only-classes)
  1. [Keep css easy to read](#keep-css-easy-to-read)

----

## Functional CSS
[1](#functional-css)

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
[1](#cascading)

- CSS (Cascading Style Sheet) becomes easier when you STOP using cascading.
- Think separation of concerns, single responsability principle, loose coupling.
- Build a whole bunch of tiny little CSS modules that:
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
[1](#style-only-classes)

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
[1](#keep-css-easy-to-read)

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

