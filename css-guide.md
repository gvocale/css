# CSS
An opinionated guide

----

## Functional CSS
## Utility classes

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
<h1 class=”Component-heading”>Hello</h1>
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
