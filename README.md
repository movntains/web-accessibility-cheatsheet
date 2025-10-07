# Web Accessibility Cheatsheet

> ⚠️This is currently a work in progress. More topics are continually being added.

Web accessibility is a vast and multi-faceted topic, so it can be easy to feel overwhelmed when you’re trying to learn how to build accessible websites. With that in mind, I've created this cheatsheet as a way to share what I've learned over years of studying accessibility and building accessible websites and web apps.

I'll do my best to explain things in plain English, since anyone who's looked at the [Web Content Accessibility Guidelines](https://www.w3.org/TR/WCAG21/) (WCAG) knows that parsing the documentation can sometimes be difficult.

I'll also include some full code examples that will hopefully be helpful, and will be as framework-agnostic as possible (although, some of the examples will intentionally be specific to frameworks like Vue or React).

If you're completely new to web accessibility, feel free to follow the [suggested reading order](#suggested-reading-order-for-newcomers). Otherwise, you can peruse the [list of topics](#list-of-topics).

## Suggested Reading Order for Accessibility Newcomers

1. [Web accessibility foundations](/foundations.md)
2. [Semantics](/semantics.md)
3. [Headings and landmarks](/headings-and-landmarks.md)
4. [Inclusive design](/inclusive-design.md)
5. [Interactivity](./interactivity.md)
6. [Animation and motion](/animation-and-motion.md)

## List of Topics

| Topic                                                   | What's Covered                                                                                                                                                                                                                                                                                                                     |
|---------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Animation and motion](/animation-and-motion.md)        | <ul><li>WCAG success criteria for motion</li><li>Implementing `prefers-reduced-motion`</li></ul>                                                                                                                                                                                                                                   |
| [Common accessibility anti-patterns](/anti-patterns.md) |                                                                                                                                                                                                                                                                                                                                    |
| [Headings and landmarks](/headings-and-landmarks.md)    | <ul><li>Outlining the page</li><li>Heading levels</li><li>Aiding navigation with landmarks</li><li>Page regions</li></ul>                                                                                                                                                                                                          |
| [Inclusive design](/inclusive-design.md)                | <ul><li>Key aspects</li><li>Touch targets</li><li>Color and contrast</li><li>Responsive design</li><li>Content reordering</li><li>Styling focus states</li></ul>                                                                                                                                                                   |
| [Interactivity](/interactivity.md)                      | <ul><li>Focus and tab order</li><li>Logical DOM order</li><li>Visibility of offscreen content</li><li>Semantic HTML elements with free keyboard support</li><li>Use a `<button>`, not a `<div>`</li><li>Links vs. buttons</li><li>Controlling focus with `tabindex`</li><li>Bypassing repetitive content with skip links</li></ul> |
| [Semantics](/semantics.md)                              | <ul><li>Affordances and semantics</li><li>Semantic HTML</li><li>Semantic properties</li><li>The accessibility tree</li></ul>                                                                                                                                                                                                       |
| [Web accessibility foundations](/foundations.md)        | <ul><li>Digital accessibility</li><li>Why web accessibility is important</li><li>Language and definitions of accessibility</li></ul>                                                                                                                                                                                               |
