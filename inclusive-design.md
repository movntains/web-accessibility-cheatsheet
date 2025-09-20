# Inclusive Design

> The need for accessibility starts **before** coding.

## Key Aspects

The following are key aspects of inclusive design:

- Bold visual contrast
- Adjustable text and layouts
- Touch targets large enough for human fingers and movement
- Obvious interactive controls
- Opt-in motion and animation (see the [animation and motion document](/animation-and-motion.md) for details)

## Touch Targets

The minimum recommended touch target size is about **48 device-independent pixels**. A `48x48` area corresponds to about 9 millimeters, which is the average size of a person's finger pad.

Touch targets should be spaced at least **8 pixels apart**, horizontally and vertically.

### Detect Touch Screen Use with Media Queries

The `pointer` CSS media feature can have a value of `fine`, `coarse`, or `none`.

It has a value of `fine` if the user is using a mouse or trackpad, even if the mouse is connected to a phone via Bluetooth.

It has a value of `coarse` if the user is using a touch screen.

It has a value of `none` if the primary input mechanism doesn't include a pointing device (e.g., voice-controlled devices).

Testing for a `coarse` pointer allows for increasing the touch targets for touch screen users, thus enabling providing a larger tap area whether the device is a phone or a larger device. Testing for width only, however, will only result in finding mobile users.

#### Example Touch Screen Detection

```css
.container a {
  padding: 0.2rem;
}

@media (pointer: coarse) {
  .container a {
    padding: 0.8rem;
  }
}
```

## Color and Contrast

### Minimum Contrast

[WCAG Success Criterion 1.4.3 Contrast (Minimum)](https://www.w3.org/TR/WCAG21/#contrast-minimum) requires a contrast ratio of at least `4.5:1` for most text.

Large scale text (at least 18 point or 14 point bold font size) requires a contrast ratio of at least `3:1`.

### Don't Convey Information with Color Alone

Most people with color deficiencies can see some or most colors, but have difficulty differentiating between certain colors, such as:

- Reds and greens (most common)
- Browns and oranges
- Blues and purples

This can result in such users missing out on certain context if said context is indicated with color alone.

For example, a form input outlined in red to display that it's invalid will not be conveyed well to a color deficient user (and won't be conveyed at all to a screen reader user).

Another example is using color only to indicate when a link is active.

## Responsive Design

By designing a site to be responsive, the UI will automatically rearrange itself for the "smaller viewport" (e.g., a larger page when a user zooms in). This is great for both desktop users who require screen magnification and mobile screen reader users.

### Using the `viewport` Meta Tag

When using the `viewport` meta tag, the following should be kept in mind:

- Setting `width=device-width` matches the screen's initial width in device-independent pixels
- Setting `initial-scale=1` establishes a `1:1` relationship between CSS pixels and device-independent pixels
- Setting `maximum-scale=1` or `user-scaleable=no` **prevents zooming**, so both options should be avoided

#### Example `viewport` Meta Tag

```html
<meta
  name="viewport"
  content="width=device-width, initial-scale=1"
>
```

### Designing with Flexibility

It's best to avoid targeting specific screen sizes. Rather, use a flexible grid and make changes to the layout when necessary.

This ensures that the design responds whether the reduced space is due to a smaller screen or a higher zoom level.

### Text Size Units

Use `em` or `rem` for text size instead of `px`.

If `px` is used, the copy will not update when the user updates text size preferences in the browser.

### Spatial Cues

Avoid using language that indicates the location of an element on the page (e.g., referring to navigation "on your left"). For one thing, this would make no sense in a mobile version. It would also be meaningless to a user who can't see the screen.

## Content Reordering

### Source Order vs. Visual Order

It's possible to reorder focusable elements using CSS (e.g., with Flexbox). However, the tab order will still be the order in which the focusable elements appear in the DOM, so the currently focused element could be jumping all over the page instead of going in a logical left-to-right order.

If content needs to be rearranged, change the order in the HTML source, not with CSS.

### CSS Properties That Can Cause Reordering

The following CSS properties commonly cause **content reordering problems**:

- `position: absolute` (takes an item out of the flow visually)
- The `order` property in Flexbox and Grid
- The `row-reverse` and `column-reverse` values for `flex-direction` in Flexbox
- The `dense` value for `grid-auto-flow` in Grid
- Any positioning by line name or number, or with `grid-template-areas` in Grid

## Styling Focus States

The focus indicator (often signified by a "focus ring") identifies the currently focused element on the page. It's **extremely important** for users who are unable to use a mouse because it acts as a stand-in for their mouse pointer.

### When to Display a Focus Indicator

A good rule of thumb is to ask, "If you clicked on this control while using a mobile device, would you expect it to display a keyboard?"

If the answer is "yes", the control should **always show** a focus indicator, regardless of the input device used to focus it. An example is the `<input>` element.

If the answer is "no", the control can **selectively show** a focus indicator. For example, a button clicked with a mouse or touch screen doesn't need a focus indicator because the action is complete. However, if the user is navigating with the keyboard, the focus indicator is used to determine if the control should be clicked or not, so a focus indicator should be displayed.

### Using `:focus` to Always Show a Focus Indicator

The `:focus` pseudo-class is applied any time an element is focused, regardless of the input device (mouse, keyboard, stylus, etc.) or the method used to focus.

It's important to note that focus is not applied the same way in all browsers. For example, [Safari, by design, does not apply focus to a `<button>` element when it's clicked](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/button#clicking_and_focus).

### Using `:focus-visible` to Selectively Show a Focus Indicator

The `:focus-visible` pseudo-class is applied any time that an element receives focus and the browser determines via heuristics that displaying a focus indicator would be beneficial to the user.

The browser will apply `:focus-visible` if the following two conditions apply:

- The most recent user interaction was via the keyboard
- The key press didn't include a meta, `Alt` / `Option`, or `Control` key

### Using `:focus-within` to Style the Parent of a Focused Element

The `:focus-within` pseudo-class is applied to an element in one of the two following cases:

- The element itself receives focus
- Another element inside the element receives focus

It can be used to highlight a region of the page to draw the user's attention to that area.

### Avoid `outline: none`

Changing the appearance of a `<button>` element with CSS or giving an element a `tabindex` will cause the browser's default focus indicator behavior to kick in.

A very common anti-pattern is to remove the focus indicator using CSS. A better way to work around the issue is to use the `:focus-visible` pseudo-class.

#### Example Accessible Focus Indicator Styling

```css
/* Hide the focus indicator for mouse users */
.button:focus {
  outline: none;
}

/* Display the focus indicator for keyboard users */
.button:focus-visible {
  outline: 2px solid blue;
  outline-offset: 2px;
}
```
