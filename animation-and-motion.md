# Using Animation and Motion Safely

When implementing motion, don't make the assumption that every user wants motion. Users should be given the option to turn motion on or off, and motion should be made **opt-in** rather than the default.

Additionally, UI animations should be designed with purpose and have a reason for being there.

Any media that autoplays should have controls that allow the user to pause or stop playback. A best practice is to not make content autoplay at all.

## WCAG Success Criteria for Motion

### Success Criterion 2.2.2 Pause, Stop, Hide

[WCAG Succession Criterion 2.2.2 Pause, Stop, Hide](https://www.w3.org/TR/WCAG21/#pause-stop-hide) addresses moving, blinking, and scrolling content. This is visible content that conveys a sense of motion.

This criterion is important for people with ADHD and other conditions (e.g., vestibular disorders) because websites with moving content can be difficult for such individuals to use.

To satisfy this criterion, mechanisms to make the motion stop must be provided.

A good rule of thumb is to use [`prefers-reduced-motion`](#implementing-prefers-reduced-motion) to prevent motion and autoplaying video from occurring in the first place.

### Success Criterion 2.3.1 Three Flashes or Below Threshold

[WCAG Succession Criterion 2.3.1 Three Flashes or Below Threshold](https://www.w3.org/TR/WCAG21/#three-flashes-or-below-threshold) states that a website shouldn't contain anything that flashes more than three times in any one-second period, or the flash is below the general flash and red flash thresholds.

This criterion is important for a variety of users because flashing content can cause nausea, seizures, migraines, and dizziness.

There's also a more strict version of this criterion, [WCAG Success Criterion 2.3.2 Three Flashes](https://www.w3.org/TR/WCAG21/#three-flashes). The difference is that there's no threshold for this criterion, so no matter what, there shouldn't be any content that flashes more than three times in any one-second period.

### Success Criterion 2.3.3 Animation from Interactions

[WCAG Success Criterion 2.3.3 Animation from Interactions](https://www.w3.org/TR/WCAG21/#animation-from-interactions) states that motion animation triggered by interaction can be disabled unless it's essential to the functionality or the information being conveyed.

This criterion typically isn't complicated to meet. All that's necessary is to make transitions and animations respond to reduced motion preferences.

## Implementing `prefers-reduced-motion`

`prefers-reduced-motion` is a media feature that can be used to detect if the user has requested that the system minimize the amount of motion it uses. It's set at the operating system level, not just in the browser.

It can be matched on `reduce` or `no-preference`. Matching on `prefers-reduced-motion: no-preference` will provide more of an opt-in approach.

### CSS Implementation

Motion preferences can be checked with a CSS media query targeting the `prefers-reduced-motion` media feature.

```css
@media (prefers-reduced-motion: reduce) {
  .animation {
    animation: none;
    transition: none;
  }
}
```

If you're a Tailwind CSS user, there are handy [`motion-safe` and `motion-reduce` variants](https://tailwindcss.com/docs/hover-focus-and-other-states#prefers-reduced-motion) that Tailwind provides.

### JavaScript Implementation

In JavaScript, the Window interface has a `matchMedia` method that can be used to detect the user's motion preferences.

```js
const motionQuery = window.matchMedia('(prefers-reduced-motion: reduce)')

function handleReduceMotionChanged() {
  if (motionQuery.matches) {
    // Adjust 'transition' or 'animation' properties
  } else {
    // Standard motion
  }
}

motionQuery.addEventListener('change', handleReduceMotionChanged)

// Trigger once on load
handleReduceMotionChanged()
```

Another instance where using JavaScript to detect motion preferences is useful is when implementing smooth scrolling.

```js
// Imagine this function being called when a button is clicked
function handleClick() {
  const prefersReducedMotion = window
    .matchMedia('(prefers-reduced-motion: reduce)')
    .matches

  window.scrollTo({
    top: 0,
    behavior: prefersReducedMotion ? 'auto' : 'smooth',
  })
}
```

A JavaScript implementation can also be helpful if motion comes from a third-party library rather than first-party CSS.

