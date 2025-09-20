# Headings and Landmarks

Screen readers have commands that enable quickly jumping between headings or to specific landmark regions. A survey found that screen reader users most often navigate an unfamiliar page by exploring the headings, so using the correct headings and landmark elements dramatically improves the navigation experience for users of assistive technologies.

## Outlining the Page

HTML headings (`<h1>` through `<h6>`) create a **structural outline** of the page. The goal is to use them to create a content hierarchy that allows anyone navigating by headings to form a mental picture of the page's content.

A common practice is the following:

- A single `<h1>` element for the primary heading
- `<h2>` elements for major sections
- `<h3>` elements in supporting subsections

### Example Page Outline via Headings

```html
<h1>Company Name</h1>

<section>
	<h2>Section Heading</h2>

	<!-- Other content -->

	<h3>Subsection Heading</h3>
</section>
```

## Heading Levels

Heading levels should increase in order, not skip around. They should also not be chosen based on text size. Skipping heading levels to use the browser's default styles that closely match the design is an anti-pattern because it breaks the outline model. Custom CSS should be used to style headings instead.

In terms of accessibility, it doesn't matter if `<h3>` elements and `<h4>` elements are visually larger than their `<h2>` element or `<h1>` element counterparts. What matters is the outline that's conveyed by the elements and their ordering.

## Aiding Navigation with Landmarks

> A landmark is a special region on the page to which a screen reader can jump.

Some elements that can (and should) be used as landmarks are `<main>`, `<nav>`, and `<aside>`. They should be used in lieu of `<div>` elements to define major sections of a page.

It's important to note that using too many landmarks can be overwhelming, so they should be used with care. For example, there should be one `<main>` element on a page rather than three or four.

## Page Regions

### Page Header

The page header typically contains **site-wide** information, such as the following:

- The website logo
- A search function
- Navigation options

The `<header>` element can be used to define this region. (It's worth noting that if it's used inside of an `<article>` element or a `<section>` element, it's not associated with the whole page, but rather with that specific element.)

#### Example Page Header

```html
<header>
	<img
		src="/images/logo.png"
		alt="Acme Corporation"
	>
</header>
```

### Page Footer

The page footer also typically contains **site-wide** information, such as the following:

- Copyright information
- Privacy statements
- Disclaimers

The `<footer>` element can be used to define this region. (It's worth noting that if it's used inside of an `<article>` element or a `<section>` element, it's not associated with the whole page, but rather with that specific element.)

#### Example Page Footer

```html
<footer>
	<p>&copy; 2025 Acme Corporation.</p>
</footer>
```

### Navigation

The `<nav>` element can be used to identify a navigation menu.

To provide better context for screen reader users, it should be given an `aria-label` or `aria-labelledby` attribute. Since a site can have multiple navigation menus (i.e., multiple `<nav>` elements), a label should be used to identify each one. Without labels, screen reader users would be left with nothing more than the announcement of `navigation` for each `<nav>` element on the page.

**Note**: When providing an `aria-label` to a `<nav>` element, do **not** include the word "navigation" in the value (e.g., `aria-label="Main Navigation"`). Screen readers will automatically add it, so including it will result in an announcement such as `Main Navigation navigation`.

#### Example Navigation

```html
<nav aria-label="Main">
	<!-- Nav content -->
</nav>

<!-- Other page content -->

<nav aria-labelledby="quicknav-heading">
	<h5 id="quicknav-heading">Quick Navigation</h5>

	<!-- Nav content -->
</nav>
```

### Main Content

The `<main>` element is used to identify the **main content region** of a website or web app.

#### Example Main Content

```html
<main>
	<h1>Stellar launch weekend for the SpaceBear 7!</h1>

	<!-- Other page content -->
</main>
```

### Complementary Content

The `<aside>` element is used to identify regions that support the main content but are separate and meaningful sections of their own (e.g., a sidenote explaining or annotating the main content).

#### Example Complementary Content

```html
<aside>
	<h3>Related Articles<h3>
</aside>
```
