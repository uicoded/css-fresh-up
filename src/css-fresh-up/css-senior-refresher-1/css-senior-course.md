# CSS Mastery Course for Senior Frontend Developers

## Course Overview
This course is designed for experienced frontend developers who want to refresh their CSS knowledge and learn about modern developments. We'll build from fundamental principles to advanced techniques, focusing on practical applications and modern best practices.

---

## Chapter 1: CSS Architecture and Methodology Foundations

### Core Principles Revisited
- **Specificity and Cascade**: Understanding the weight system (inline: 1000, IDs: 100, classes: 10, elements: 1)
- **Inheritance**: Which properties inherit and how to control it
- **Box Model**: Content, padding, border, margin - and `box-sizing`

### Modern CSS Methodologies
- **BEM (Block Element Modifier)**: `.block__element--modifier`
- **OOCSS**: Separating structure from skin, container from content
- **SMACSS**: Base, Layout, Module, State, Theme
- **CSS-in-JS considerations**: When and why to use it

**Example**: [BEM Methodology on CodePen](https://codepen.io/pen?template=BaRqXaJ)

```css
/* BEM Example */
.card { /* Block */ }
.card__header { /* Element */ }
.card__header--featured { /* Modifier */ }
```

---

## Chapter 2: Modern Layout Systems

### CSS Grid - The Layout Revolution
Grid fundamentally changed how we approach layout. Unlike flexbox (1-dimensional), Grid is 2-dimensional.

**Key Concepts:**
- Grid containers and grid items
- Grid lines, tracks, cells, and areas
- Implicit vs explicit grids

```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  grid-gap: 1rem;
}
```

**Examples:**
- [CSS Grid Complete Guide](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [Grid by Example](https://gridbyexample.com/)

### Advanced Flexbox Patterns
While Grid handles 2D layouts, Flexbox excels at 1D layouts and component-level alignment.

```css
.flex-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem; /* Modern gap property */
}
```

### Subgrid (New!)
Allows nested grids to inherit parent grid tracks.

```css
.parent {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}

.child {
  display: grid;
  grid-template-columns: subgrid; /* Inherits parent's columns */
}
```

---

## Chapter 3: Advanced Selectors and Pseudo-Classes

### Modern Pseudo-Classes
- `:is()` and `:where()` - Logical pseudo-classes
- `:has()` - Parent selector (CSS4)
- `:focus-visible` - Better focus management
- `:focus-within` - Container focus states

```css
/* :is() reduces repetition */
:is(h1, h2, h3, h4) {
  margin-top: 2rem;
}

/* :has() - parent selector */
.card:has(.featured-badge) {
  border: 2px solid gold;
}

/* :focus-visible for better UX */
button:focus-visible {
  outline: 2px solid blue;
}
```

### Advanced Attribute Selectors
```css
/* Substring matching */
[class*="btn"] { /* Contains "btn" */ }
[href^="https"] { /* Starts with "https" */ }
[src$=".jpg"] { /* Ends with ".jpg" */ }
```

---

## Chapter 4: Custom Properties (CSS Variables) Deep Dive

### Beyond Basic Variables
CSS Custom Properties are more powerful than Sass variables because they're live in the DOM.

```css
:root {
  --primary-color: #007bff;
  --spacing-unit: 8px;
  --border-radius: calc(var(--spacing-unit) / 2);
}

/* Scoped variables */
.dark-theme {
  --primary-color: #66b3ff;
  --bg-color: #1a1a1a;
}
```

### Advanced Techniques
- **Fallback values**: `var(--color, #000)`
- **Type checking**: Using `@property` for typed custom properties
- **Animation with custom properties**

```css
@property --rotation {
  syntax: '<angle>';
  initial-value: 0deg;
  inherits: false;
}

.element {
  transform: rotate(var(--rotation));
  transition: --rotation 0.3s ease;
}
```

---

## Chapter 5: Modern Typography and Text Layout

### Variable Fonts
Single font files with multiple variations (weight, width, slant).

```css
@font-face {
  font-family: 'Inter Variable';
  src: url('inter-variable.woff2') format('woff2-variations');
  font-weight: 100 900;
  font-stretch: 50% 200%;
}

.text {
  font-family: 'Inter Variable';
  font-weight: 450; /* Any value between 100-900 */
  font-variation-settings: 'wght' 450, 'slnt' -10;
}
```

### Advanced Text Features
- `text-wrap: balance` - Better headline wrapping
- `text-wrap: pretty` - Improved paragraph flow
- `initial-letter` - Drop caps
- `font-feature-settings` - OpenType features

```css
h1 {
  text-wrap: balance;
}

p {
  text-wrap: pretty;
}

.drop-cap::first-letter {
  initial-letter: 3;
  font-weight: bold;
  color: var(--accent-color);
}
```

---

## Chapter 6: Container Queries - The Game Changer

Container queries allow components to respond to their container's size, not the viewport.

```css
.card-container {
  container-type: inline-size;
  container-name: card;
}

@container card (min-width: 400px) {
  .card {
    display: flex;
    gap: 1rem;
  }
  
  .card__image {
    flex: 0 0 200px;
  }
}
```

**Example**: [Container Queries Demo](https://codepen.io/una/pen/mdByMPP)

### Container Query Units
- `cqw` - Container query width
- `cqh` - Container query height  
- `cqi` - Container query inline size
- `cqb` - Container query block size

---

## Chapter 7: Advanced Color and Gradients

### Modern Color Functions
- `oklch()` - Perceptually uniform color space
- `color-mix()` - Mix colors in CSS
- `light-dark()` - Automatic dark mode colors

```css
:root {
  --primary: oklch(0.7 0.15 200); /* Lightness, Chroma, Hue */
  --accent: color-mix(in oklch, var(--primary), white 20%);
}

@media (prefers-color-scheme: dark) {
  --bg: light-dark(white, #1a1a1a);
  --text: light-dark(#333, white);
}
```

### Advanced Gradients
```css
.gradient {
  background: conic-gradient(
    from 45deg at 50% 50%,
    #ff6b6b 0deg,
    #4ecdc4 120deg,
    #45b7d1 240deg,
    #ff6b6b 360deg
  );
}
```

---

## Chapter 8: Animations and Transitions Mastery

### CSS Animations Performance
Understanding the rendering pipeline and what properties are cheap to animate.

**Cheap to animate (compositor only):**
- `transform`
- `opacity`
- `filter`

**Expensive (triggers layout/paint):**
- `width`, `height`
- `top`, `left`
- `border-width`

### Advanced Animation Techniques
```css
@keyframes slideInUp {
  from {
    transform: translate3d(0, 100%, 0);
    opacity: 0;
  }
  to {
    transform: translate3d(0, 0, 0);
    opacity: 1;
  }
}

.element {
  animation: slideInUp 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  /* Using custom easing curves */
}
```

### View Transitions API
Smooth transitions between page states.

```css
::view-transition-old(root),
::view-transition-new(root) {
  animation-duration: 0.5s;
}

::view-transition-old(root) {
  animation-name: slide-out;
}

::view-transition-new(root) {
  animation-name: slide-in;
}
```

---

## Chapter 9: Responsive Design Evolution

### Modern Responsive Patterns
Moving beyond device-specific breakpoints to content-driven design.

```css
/* Intrinsic responsive design */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(300px, 100%), 1fr));
  gap: 1rem;
}

/* Container-based responsive */
@container (min-width: 768px) {
  .component {
    /* Styles based on container, not viewport */
  }
}
```

### Logical Properties
Writing mode and direction independent properties.

```css
.element {
  margin-inline: 1rem; /* margin-left and margin-right */
  margin-block: 2rem;  /* margin-top and margin-bottom */
  padding-inline-start: 1rem; /* padding-left in LTR */
  border-inline-end: 1px solid; /* border-right in LTR */
}
```

---

## Chapter 10: CSS Architecture at Scale

### Layer Management
CSS `@layer` for managing cascade and specificity.

```css
@layer reset, base, components, utilities;

@layer reset {
  * { margin: 0; padding: 0; }
}

@layer base {
  body { font-family: system-ui; }
}

@layer components {
  .btn { /* Component styles */ }
}
```

### CSS Scoping
- `@scope` rule for style encapsulation
- `:scope` pseudo-class

```css
@scope (.card) to (.card__content) {
  :scope {
    border: 1px solid #ccc;
  }
  
  h2 {
    /* Only affects h2 within .card but not in .card__content */
  }
}
```

---

## Chapter 11: Performance and Optimization

### CSS Loading Performance
- Critical CSS inlining
- CSS containment with `contain` property
- `content-visibility` for rendering optimization

```css
.off-screen-content {
  content-visibility: auto;
  contain-intrinsic-size: 0 500px;
}
```

### Modern CSS Units
- `dvh`, `svh`, `lvh` - Dynamic viewport units
- `ch`, `ex` - Typography-relative units
- Container query units (`cqw`, `cqh`, etc.)

```css
.hero {
  height: 100dvh; /* Dynamic viewport height */
  padding: 2ch; /* 2 character widths */
}
```

---

## Chapter 12: CSS Houdini and the Future

### CSS Houdini APIs
Extending CSS with JavaScript.

```css
/* Custom paint worklet */
.element {
  background: paint(my-custom-paint);
}
```

```javascript
// paint-worklet.js
class MyCustomPaint {
  paint(ctx, geom, properties) {
    // Custom painting logic
  }
}

registerPaint('my-custom-paint', MyCustomPaint);
```

### Emerging Features
- CSS Nesting (native, similar to Sass)
- CSS Functions (`round()`, `mod()`, `rem()`)
- Cascade layers with `@layer`

---

## Practical Exercises

### Exercise 1: Modern Layout Challenge
Create a responsive card grid using CSS Grid with container queries.

### Exercise 2: Dark Mode Implementation
Implement a comprehensive dark mode using custom properties and `light-dark()`.

### Exercise 3: Animation Performance Audit
Optimize a heavy animation by moving expensive properties to compositor-only changes.

---

## Resources and References

### Essential Reading
- [MDN CSS Reference](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [CSS Tricks Guides](https://css-tricks.com/guides/)
- [Can I Use](https://caniuse.com/) - Browser support tables

### Stay Updated
- [CSS Working Group Specs](https://www.w3.org/Style/CSS/)
- [Chrome Platform Status](https://chromestatus.com/features#css)
- [Firefox Developer Edition](https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases)

### Tools
- **PostCSS** - CSS transformation
- **Stylelint** - CSS linting
- **PurgeCSS** - Remove unused CSS
- **Critical** - Extract critical CSS

---

## Conclusion

CSS has evolved dramatically in recent years. Modern CSS provides powerful layout systems, sophisticated styling capabilities, and performance optimizations that were previously impossible or required JavaScript solutions. The key is understanding when and how to use these new features while maintaining browser support and performance standards.

Focus on progressive enhancement: start with solid fundamentals, then layer on modern features where they provide clear benefits. Remember that CSS architecture becomes more important as applications scale - invest time in establishing consistent patterns and naming conventions from the start.
