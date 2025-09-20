# Semantics

A key aspect of web accessibility is semantics. If you've been in web development for any length of time, you've likely heard the term "semantic HTML" before. This document will explain what that is and how it relates to accessibility.

## Affordances and Semantics

### Affordances

> An affordance is any object that offers, or affords, its user the opportunity to perform an action.

Let's look at a simple example.

The physical design of a teapot conveys to the user how it should be operated. It has a handle, and a person has seen objects with similar handles. Therefore, they can infer how it should be picked up and operated.

How does this relate to websites and accessibility?

When building graphical user interfaces (GUIs), CSS is used to add **visual affordances** to a UI. For example, a button may be given a drop shadow and border so it resembles an actual physical button.

However, these visual affordances aren't conveyed to users who can't see the screen, so the UI must be constructed in such a way that it conveys the same affordances to assistive technologies. This is where semantics comes in.

### Semantics

Semantics is the **non-visual** exposure of a UI element's affordances.

## Semantic HTML

The easiest way to convey proper semantics is using semantically rich HTML elements.

Using semantic HTML elements provides better support for assistive technologies (ATs) by default, so it ends up requiring less work than adding accessibility features manually.

Let's take a look at an example.

It's possible to style a `<div>` and a `<button>` so that they convey the same visual affordances, but the experiences are very different when using a screen reader. A `<div>` is a generic grouping element, so a screen reader only announces its text content. A `<button>`, however, is announced as a "button", which is a much stronger signal to the user that it's something with which they can interact.

The simplest and best solution is to **avoid custom interactive controls** altogether. For example, replace a `<div>` that's acting like a button with an actual `<button>` element.

### Examples of Semantic HTML Elements

- `<ul>`
- `<ol>`
- `<p>`
- `<button>`
- `<table>`
- `<figure>`
- `<hr>`
- `<select>`

## Semantic Properties

Generally speaking, every HTML element has some of the following semantic properties:

- Role or type
- Name
- Value (optional)
- State (optional)

### Role

An HTML element's role describes its **type**.

Some examples are the following:

- Button
- Input
- Group (for elements like `<div>` and `<span>`)

### Name

An HTML element's name is its **computed label**.

Screen readers typically announce an element's name followed by its role (e.g., `Sign Up, button`).

The algorithm that determines an element's name factors in the following:

- If there's any text content inside the element
- If it has attributes such as `title` or `placeholder`
- If it's associated with an actual `<label>` element
- If it has any ARIA attributes, such as `aria-label` or `aria-labelledby`

### Value

An HTML element's value is just that -- its value (e.g., what the user has typed into a text input).

### State

An HTML element's state conveys its **current status**.

For example, a `<select>` element can be in an `expanded` or `collapsed` state, depending upon if it's open or closed.

## The Accessibility Tree

The accessibility tree is essentially the bridge between the DOM and assistive technologies. For each node in the DOM, the browser determines if the node is semantically "interesting" and adds the node to the accessibility tree if it's deemed as such.

Assistive technologies often provide an alternative UI to the user by walking the accessibility tree. For example, a screen reader can provide a list of headings, links, or interactive elements found on the page.

Browsers often **remove semantically uninteresting nodes** like `<div>` and `<span>` from the accessibility tree, especially if they're only being used to position their children with CSS. For example, if a `<button>` element is nested inside of 5 `<div>` elements, the browser may prune some of the `<div>` elements in the middle to cut down on noise.
