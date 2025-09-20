# Common Accessibility Anti-Patterns

These are some common accessibility anti-patterns that should be avoided. A solution is provided for each anti-pattern.

## Anti-Pattern #1

🚫 *Anti-pattern*: Skipping heading levels to use the browser's default styles that closely match the design.

✅ *Solution*: Use custom CSS to change the heading styles.

## Anti-Pattern #2

🚫 *Anti-pattern*: Using CSS to change the order of elements on the page.

✅ *Solution*: Make the DOM order match the visual order.

## Anti-Pattern #3

🚫 *Anti-pattern*: Treating a non-interactive element (e.g., `<div>` or `<span>`) as a button by adding a click handler to it.

✅ *Solution*: Use the `<button>` element instead.

## Anti-Pattern #4

🚫 *Anti-pattern*: Treating links as buttons by attaching JavaScript behavior to them.

✅ *Solution*: Use the `<button>` element if clicking on the element will perform an action on the page.

## Anti-Pattern #5

🚫 *Anti-pattern*: Giving an element a `tabindex` greater than `0`.

✅ *Solution*: Move the element that needs to come earlier in the tab order to an earlier spot in the DOM.

## Anti-Pattern #6

🚫 *Anti-pattern*: Removing an element's focus indicator with CSS.

✅ *Solution*: Use the `:focus-visible` pseudo-class.
