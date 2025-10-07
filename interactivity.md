# Interactivity and Keyboard Accessibility

> Anything that a mouse user can do, a keyboard and screen reader user must also be able to do.

The interaction doesn't need to be exactly the same, but someone using assistive technologies must have a way to complete the task. For this reason, keyboard-operable elements must be reachable with `Tab`. (It's worth noting that some browsers, like Safari, require updating settings in order for this to be possible.)

When semantic HTML doesn't suffice on its own, JavaScript and DOM events can be used to add functionality. This tends to be necessary for more complex UI functionality, such as drag-and-drop.

## Focus and Tab Order

**Focus** refers to which element in the application (e.g., a form field, checkbox, button, link) currently **receives input** from the keyboard.

The currently focused element is often indicated by a **focus indicator**, which is styled differently in different browsers. [Properly styled focus indicators](/inclusive-design.md#styling-focus-states) are essential for keyboard accessibility.

**Tab order** is the order in which focus proceeds forward and backward through interactive elements. `Tab` navigates forward through the elements, while `Shift + Tab` navigates backwards.

Interactive HTML elements (e.g., text fields, buttons, select lists) are **implicitly focusable**. They're automatically inserted into the tab order based on their position in the DOM, and they also have built-in keyboard event handling.

Elements such as `<p>` and `<div>` are not implicitly focusable because users typically don't need to interact with them.

There are two main ideas to keep in mind when assessing and adjusting tab order:

- Arrange elements in the DOM to be in a logical order
- Correctly set the visibility of offscreen content that should not receive focus

> 💥 **Tip**
> 
> To find the element that currently has focus, enter `document.activeElement` in the browser console.

## Logical DOM Order

In general, focus should follow reading order (left to right, top to bottom in Western cultures).

If the focus order seems wrong, rearrange the elements in the DOM to make the tab order more natural. If something should appear to be **visually earlier** on the screen, move it **earlier in the DOM**.

Changing the visual position of elements with CSS can create an illogical tab order, and should be avoided.

### Example of a Logical Tab Order

```html
<button>Kiwi</button>
<button>Peach</button>
<button>Coconut</button>
```

In this example, the tab order is logical because the buttons are arranged in a left-to-right order that matches the reading order.

### Example of an Illogical Tab Order

```html
<button style="float: right;">Kiwi</button>
<button>Peach</button>
<button>Coconut</button>
```

In this example, the tab order is illogical because the `Kiwi` button is the first button in the DOM, but `style="float: right;"` makes it visually appear as the last button. A keyboard user would tab through the buttons in the order `Peach`, `Coconut`, `Kiwi`, which would be confusing.

Rather than using `style="float: right;"` to make the `Kiwi` button appear on the right, the `<button>` element for `Kiwi` should be moved after the `Coconut` button in the DOM and the inline style should be removed.

## Visibility of Offscreen Content

Sometimes, offscreen interactive elements need to be in the DOM but should **not** be in the tab order. For example, if there's a responsive sidenav that opens when a button is clicked, the user shouldn't be able to focus on the elements within the sidenav when it's closed.

To prevent an interactive element from receiving focus, it should be given either of the following CSS properties:

- `display: none;`
- `visibility: hidden;`

To add the element back into the tab order (e.g., when the sidenav is open), replace the above CSS properties, respectively, with:

- `display: block;` (or another appropriate `display` value)
- `visibility: visible;`

## Semantic HTML Elements with Free Keyboard Support

Some HTML elements provide keyboard interactivity for free, such as:

- `<button>`
- `<a>` (with a valid `href` attribute)
- `<input>` (and its many types)
- `<select>`
- `<textarea>`
- `<details>`

These elements are **implicitly focusable** and have built-in keyboard event handling. For example, a `<button>` can be activated with both `Enter` and `Space`, while a link (`<a>`) can be activated with `Enter`.

When possible, use these semantic HTML elements instead of non-semantic elements like `<div>` and `<span>`, which require additional work to make them accessible.

Built-in semantic elements have unique interactions on mobile devices, and attempting to reproduce them is a lot of work. This is another reason why it's best to stick to built-in elements whenever possible.

It's worth noting that elements with the `contenteditable` attribute are sometimes used for freeform text entry. If it's set to `true` or an empty string, then the element is editable.

## Use a `<button>`, Not a `<div>`

Treating a non-interactive element (e.g., `<div>` or `<span>`) as a button by adding a click handler to it is a common accessibility anti-pattern.

To be considered accessible, a button should:

- Be focusable via the keyboard
- Support being disabled
- Support the `Enter` and `Space` keys to perform an action
- Be announced properly by a screen reader

A `<div>` button has none of these properties, so additional code would be needed to replicate what the `<button>` element provides for free.

`<button>` elements have **synthetic click activation**, which means that a `<button>` element's click handler will run when the user presses `Enter` or `Space`.

A `<div>` element does not have synthetic click activation, so additional code would be required to do the following:

- Listen for the `keydown` event
- Check that the keycode is `Enter` or `Space`
- Run the click handler when the correct key is pressed

## Links vs. Buttons

Treating links as buttons by attaching JavaScript behavior to them is another common anti-pattern.

Both buttons and links support some form of synthetic click activation, but they have different default behaviors and purposes.

If clicking on an element results in **performing an action**, use a `<button>` element.

If clicking on an element results in **navigating** the user to a new page (or to a specific section on the current page), use an `<a>` element with a valid `href` attribute. This includes single-page applications (SPAs) that load new content and update the URL using the [History API](https://developer.mozilla.org/en-US/docs/Web/API/History_API).

Screen readers announce buttons and links differently, so using the correct element helps screen reader users know which outcome to expect.

## Controlling Focus with `tabindex`

### Checking Keyboard Accessibility of Controls

If pressing `Tab` doesn't allow for reaching all of the interactive controls on a page, `tabindex` will need to be used to improve the focusability of those controls, or they will need to be updated to use semantic HTML elements (if possible).

If no focus indicator is visible, it's likely hidden by CSS with `:focus { outline: none; }`.

### Inserting an Element into the Tab Order

`tabindex="0"` can be added to an element to make it focusable and insert it into the natural tab order. To focus the element, press `Tab` or call its `focus()` method.

#### Example of Inserting an Element into the Tab Order

```html
<div tabindex="0">Focus me with the Tab key</div>
```

### Removing an Element from the Tab Order

`tabindex="-1"` can be added to an element to make it focusable with JavaScript and remove it from the tab order. It can be programmatically focused by calling its `focus()` method, but it cannot be reached with the `Tab` key.

Applying `tabindex="-1"` to an element doesn't affect its children. If they're in the tab order naturally or because of `tabindex="0"`, they'll remain in the tab order and will be reachable with `Tab`.

#### Example of Removing an Element from the Tab Order

```html
<button tabindex="-1">Can't reach me with the Tab key</button>
```

### Avoid `tabindex` Greater Than 0

Any `tabindex` value greater than `0` will move the element to the front of the natural tab order. If there are multiple elements with a `tabindex` greater than `0`, the tab order starts from the lowest value greater than `0` and works its way up.

Using a `tabindex` greater than `0` is considered an anti-pattern because it creates a confusing and illogical tab order. Screen readers navigate the page in DOM order, not tab order, so using a `tabindex` greater than `0` can create a disjointed experience for screen reader users. If an element needs to come sooner in the tab order, it should be moved to an earlier spot in the DOM.

### Creating Accessible Components with Roving `tabindex`

Complex components may require additional keyboard support beyond focus. For example, the native `<select>` element is focusable and the arrow keys can be used to expose additional functionality (i.e., the selectable options).

**Roving tabindex** is a technique that sets `tabindex="-1"` for all children except the currently active one. This allows the user to navigate between the children using arrow keys, while still allowing the user to tab into and out of the component.

The component uses a keyboard event listener to determine which key the user has pressed. When this happens, the component does the following:

- Sets the previously focused child's `tabindex` to `-1`
- Sets the to-be-focused child's `tabindex` to `0`
- Calls the to-be-focused child's `focus()` method

#### Example of Roving `tabindex`

```html
<!-- Before using the arrow key to move from "Redo" to "Cut" -->
<div role="toolbar">
  <button tabindex="-1">Undo</button>
  <button tabindex="0">Redo</button>
  <button tabindex="-1">Cut</button>
</div>
```

```html
<!-- After using the arrow key to move from "Redo" to "Cut" -->
<div role="toolbar">
  <button tabindex="-1">Undo</button>
  <button tabindex="-1">Redo</button>
  <button tabindex="0">Cut</button>
</div>
```

## Bypassing Repetitive Content with Skip Links

A **skip link** is an offscreen link that is always the _first focusable element_ in the DOM. It allows keyboard and screen reader users to bypass repetitive content (e.g., a navigation menu) and jump straight to the main content of a page.

It typically contains an in-page link to the main content of the page, and can be focused when the user presses `Tab` after first accessing a web page.

Since it's the first focusable element in the DOM, it takes a single action from assistive technologies to focus it and bypass repetitive content, which greatly improves the user experience for people who use assistive technologies.

### Example of a Skip Link

```html
<!-- index.html -->

<a
  href="#main"
  class="skip-link"
>
  Skip to Main Content
</a>

<!-- Other content (e.g., a <nav> element) -->

<main id="main">
  <!-- Main content -->
</main>
```

```css
/* styles.css */

.skip-link {
  position: absolute;
  top: -40px; /* Hide offscreen */
  left: 0;
  background: #000000;
  color: #ffffff;
  padding: 8px;
  z-index: 100;
}

.skip-link:focus {
  top: 0; /* Bring onscreen when focused */
}
```
