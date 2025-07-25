# Inheritance

CSS inheritance is a fundamental mechanism where child elements automatically receive certain property values from their parent elements, creating a cascading effect down the DOM tree. This helps maintain consistency and reduces the need to explicitly set every property on every element.

## Which Properties Inherit by Default

CSS properties fall into two categories regarding inheritance:

### **Inherited Properties** (automatically passed down)

These are primarily **text and typography-related** properties:

```css
/* Typography */
font-family, font-size, font-weight, font-style, font-variant
line-height, letter-spacing, word-spacing, text-align, text-indent
text-transform, white-space, color

/* Lists */
list-style, list-style-type, list-style-position, list-style-image

/* Tables */
border-collapse, border-spacing, caption-side, empty-cells

/* Miscellaneous */
cursor, visibility, quotes
```

**Example of natural inheritance:**

```css
body {
  font-family: 'Inter', sans-serif;
  font-size: 16px;
  color: #333;
  line-height: 1.6;
}

/* All text elements (h1, p, span, etc.) will inherit these values */
```

### **Non-Inherited Properties** (not passed down)

These are primarily **layout, spacing, and visual** properties:

```css
/* Box Model */
width, height, margin, padding, border

/* Positioning */
position, top, right, bottom, left, z-index

/* Display & Layout */
display, float, clear, overflow, flex properties, grid properties

/* Background & Visual Effects */
background, box-shadow, border-radius, opacity, transform

/* Others */
vertical-align, text-decoration
```

## Controlling Inheritance

CSS provides several keyword values to explicitly control inheritance:

### **The Four Inheritance Keywords**

```css
.element {
  /* 1. inherit - Force inheritance from parent */
  border: inherit; /* Takes parent's border value */
  
  /* 2. initial - Reset to property's default value */
  color: initial; /* Usually black for color */
  
  /* 3. unset - inherit if inheritable, initial if not */
  margin: unset; /* Becomes initial (0) since margin doesn't inherit */
  color: unset;  /* Becomes inherited since color inherits */
  
  /* 4. revert - Use browser/user stylesheet value */
  font-size: revert; /* Browser's default, usually 16px */
}
```

### **Practical Examples**

**Forcing inheritance on non-inherited properties:**

```css
.parent {
  border: 2px solid blue;
}

.child {
  border: inherit; /* Child will have the same border as parent */
}
```

**Creating a "reset" pattern:**

```css
.component {
  /* Reset all properties to their initial values */
  all: initial;
  
  /* Then apply only what you need */
  display: block;
  font-family: inherit; /* Re-inherit typography from ancestor */
}
```

**Managing inheritance in component libraries:**

```css
.button {
  /* Don't inherit text styles from parent context */
  font-family: system-ui, sans-serif;
  font-size: 14px;
  color: initial;
  
  /* But do respect user's cursor preferences */
  cursor: inherit;
}
```

## Advanced Inheritance Patterns

### **Creating Inheritance Chains**

```css
.theme-container {
  --primary-color: #007bff;
  --text-color: #333;
  --border-style: solid;
}

.card {
  color: var(--text-color); /* Inherits custom property */
  border-color: var(--primary-color);
  border-style: var(--border-style);
}
```

### **Selective Inheritance Control**

```css
.isolated-component {
  /* Block most inheritance */
  all: initial;
  
  /* Selectively re-inherit useful properties */
  font-family: inherit;
  direction: inherit; /* For RTL support */
  cursor: inherit;
}
```

### **Managing Inheritance in Dark Mode**

```css
.dark-theme {
  color-scheme: dark;
  --text-color: #fff;
  --bg-color: #1a1a1a;
}

.content {
  /* These will inherit the theme colors */
  color: inherit;
  background-color: var(--bg-color);
}

.button {
  /* Override inheritance when needed */
  color: var(--button-color, inherit);
  background: var(--button-bg, transparent);
}
```

## Common Inheritance Pitfalls and Solutions

### **Problem: Unwanted inheritance**

```css
/* Problem: All elements inherit red color */
.error-container {
  color: red;
}

/* Solution: Scope the color more specifically */
.error-container {
  border: 2px solid red;
}

.error-container .error-message {
  color: red; /* Only apply to specific elements */
}
```

### **Problem: Breaking inheritance chains**

```css
/* Problem: This breaks font inheritance */
.component * {
  font-family: Arial; /* Too broad */
}

/* Solution: Use more specific selectors */
.component {
  font-family: Arial; /* Let inheritance work naturally */
}
```

## Modern Best Practices

### **Use Custom Properties for Inheritance**

```css
:root {
  --font-family-base: system-ui, sans-serif;
  --font-family-mono: 'Fira Code', monospace;
  --line-height-base: 1.6;
}

body {
  font-family: var(--font-family-base);
  line-height: var(--line-height-base);
}

code {
  font-family: var(--font-family-mono);
  line-height: inherit; /* Inherit line-height but override font */
}
```

### **Logical Properties for Better Inheritance**

```css
.text-content {
  /* These respect writing mode and direction inheritance */
  margin-block: 1rem;
  padding-inline: 1rem;
  text-align: start; /* Inherits text direction */
}
```

Understanding inheritance helps you write more maintainable CSS by leveraging the cascade effectively, reducing redundancy, and creating more predictable styling patterns. The key is knowing when to let inheritance work naturally and when to override it for specific design needs.