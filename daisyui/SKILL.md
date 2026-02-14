---
name: daisyui
description: Use when building with DaisyUI — Tailwind CSS component class library. Covers class naming conventions, component classes (btn, card, modal, drawer, tab, badge, alert, etc.), color modifiers, size modifiers, theming with data-theme and CSS variables, OKLch colors, responsive patterns, installation, and class reference lookup via MCP tools.
---

# DaisyUI

## 1. Overview

DaisyUI is a **CSS component class library** for Tailwind CSS. Instead of writing long utility class strings, you use semantic class names like `btn`, `card`, `modal`. It provides **65+ components** with consistent theming through CSS variables and `data-theme` attributes.

All DaisyUI class references and examples are available through the `frontend-components` MCP server under the `daisyui` framework.

## 2. Installation

```bash
npm install daisyui
```

### Tailwind CSS v4

```css
@import "tailwindcss";
@plugin "daisyui";
```

### Tailwind CSS v3

```js
// tailwind.config.js
module.exports = {
  plugins: [require("daisyui")],
}
```

## 3. MCP Workflow

### 3.1 Browse All Components

```
list_components(framework: "daisyui")
```

Returns all 65 component reference files.

### 3.2 Get Component Reference

```
# Get full class reference + examples for a component
get_component(framework: "daisyui", category: "components", component_type: "all", variant: "button")
get_component(framework: "daisyui", category: "components", component_type: "all", variant: "card")
get_component(framework: "daisyui", category: "components", component_type: "all", variant: "modal")
```

### 3.3 Search Components

```
search_components(query: "input", framework: "daisyui")
search_components(query: "nav", framework: "daisyui")
```

## 4. Class Naming Conventions

### 4.1 Base Classes

Every component has a base class that applies the default styles:

| Component | Base Class | Purpose |
|-----------|-----------|---------|
| Button | `btn` | Clickable button element |
| Card | `card` | Content container with padding |
| Modal | `modal` | Dialog overlay |
| Drawer | `drawer` | Side panel |
| Navbar | `navbar` | Top navigation bar |
| Footer | `footer` | Page footer |
| Tab | `tab` | Tab navigation item |
| Badge | `badge` | Small status indicator |
| Alert | `alert` | Notification banner |
| Table | `table` | Data table |
| Menu | `menu` | Vertical or horizontal menu |
| Dropdown | `dropdown` | Dropdown container |
| Tooltip | `tooltip` | Hover tooltip |
| Toggle | `toggle` | Toggle switch |
| Checkbox | `checkbox` | Checkbox input |
| Radio | `radio` | Radio input |
| Input | `input` | Text input field |
| Select | `select` | Select dropdown |
| Textarea | `textarea` | Multi-line input |
| Range | `range` | Range slider |
| Rating | `rating` | Star rating |
| Progress | `progress` | Progress bar |
| Loading | `loading` | Loading spinner |
| Collapse | `collapse` | Collapsible content |
| Accordion | `accordion` | Accordion group |
| Carousel | `carousel` | Image/content slider |
| Countdown | `countdown` | Timer countdown |
| Diff | `diff` | Before/after comparison |
| Divider | `divider` | Content separator |
| Indicator | `indicator` | Corner badge/notification |
| Join | `join` | Group items together |
| Kbd | `kbd` | Keyboard key display |
| Link | `link` | Styled anchor link |
| Mask | `mask` | Shape mask for images |
| Mockup | `mockup-browser`, `mockup-code`, `mockup-phone`, `mockup-window` | Device mockups |
| Skeleton | `skeleton` | Loading placeholder |
| Stack | `stack` | Stacked elements |
| Stat | `stat` | Statistics display |
| Steps | `steps` | Step indicator |
| Swap | `swap` | Content toggle |
| Toast | `toast` | Toast notification |
| Timeline | `timeline` | Event timeline |
| Hero | `hero` | Hero section |

### 4.2 Color Modifiers

DaisyUI uses semantic color names. Apply with `{component}-{color}`:

| Color | Purpose | Example |
|-------|---------|---------|
| `primary` | Main brand action | `btn-primary` |
| `secondary` | Secondary actions | `btn-secondary` |
| `accent` | Accent/highlight | `badge-accent` |
| `neutral` | Neutral/default | `btn-neutral` |
| `info` | Informational | `alert-info` |
| `success` | Success state | `alert-success` |
| `warning` | Warning state | `alert-warning` |
| `error` | Error/danger state | `alert-error` |
| `ghost` | Transparent/subtle | `btn-ghost` |

### 4.3 Size Modifiers

Consistent sizing across components:

| Size | Modifier | Example |
|------|----------|---------|
| Extra small | `-xs` | `btn-xs` |
| Small | `-sm` | `btn-sm` |
| Medium (default) | `-md` | `btn-md` |
| Large | `-lg` | `btn-lg` |
| Extra large | `-xl` | `btn-xl` |

### 4.4 Style Modifiers

| Style | Modifier | Example |
|-------|----------|---------|
| Outline | `-outline` | `btn-outline` |
| Dash | `-dash` | `btn-dash` |
| Soft | `-soft` | `btn-soft` |
| Ghost | `-ghost` | `btn-ghost` |
| Link | `-link` | `btn-link` |
| Glass | `glass` | `btn glass` |

### 4.5 Shape Modifiers

| Shape | Modifier | Example |
|-------|----------|---------|
| Wide | `-wide` | `btn-wide` |
| Block (full width) | `-block` | `btn-block` |
| Square (1:1) | `-square` | `btn-square` |
| Circle | `-circle` | `btn-circle` |

## 5. Theming

### 5.1 Built-in Themes

DaisyUI includes 30+ built-in themes. Apply with `data-theme` attribute:

```html
<html data-theme="light">
<html data-theme="dark">
<html data-theme="cupcake">
<html data-theme="retro">
<html data-theme="cyberpunk">
<html data-theme="valentine">
<html data-theme="garden">
<html data-theme="forest">
<html data-theme="lofi">
<html data-theme="dracula">
<html data-theme="business">
<html data-theme="night">
```

### 5.2 Theme Scope

Themes can be scoped to any element, not just `<html>`:

```html
<div data-theme="dark">
  <!-- Dark themed section -->
  <button class="btn btn-primary">Dark button</button>
</div>
<div data-theme="light">
  <!-- Light themed section -->
  <button class="btn btn-primary">Light button</button>
</div>
```

### 5.3 Custom Themes

Define custom themes using CSS variables with OKLch color values:

```css
[data-theme="mytheme"] {
  --color-primary: oklch(65% 0.25 260);
  --color-primary-content: oklch(98% 0 0);
  --color-secondary: oklch(70% 0.2 180);
  --color-secondary-content: oklch(98% 0 0);
  --color-accent: oklch(75% 0.18 80);
  --color-accent-content: oklch(20% 0 0);
  --color-neutral: oklch(30% 0.02 260);
  --color-neutral-content: oklch(95% 0 0);
  --color-base-100: oklch(98% 0.01 260);
  --color-base-200: oklch(95% 0.01 260);
  --color-base-300: oklch(90% 0.01 260);
  --color-base-content: oklch(20% 0.02 260);
  --color-info: oklch(70% 0.15 230);
  --color-success: oklch(70% 0.2 150);
  --color-warning: oklch(80% 0.18 80);
  --color-error: oklch(65% 0.25 25);
  --radius-selector: 0.5rem;
  --radius-field: 0.25rem;
  --radius-box: 0.5rem;
  --size-selector: 0.25rem;
  --size-field: 0.25rem;
  --border: 1px;
  --depth: 1;
  --noise: 0;
}
```

### 5.4 CSS Variables Reference

| Variable | Purpose |
|----------|---------|
| `--color-primary` | Primary brand color |
| `--color-primary-content` | Text on primary |
| `--color-secondary` | Secondary color |
| `--color-accent` | Accent color |
| `--color-neutral` | Neutral color |
| `--color-base-100` | Base background |
| `--color-base-200` | Slightly darker bg |
| `--color-base-300` | Even darker bg |
| `--color-base-content` | Text on base |
| `--color-info` | Info state |
| `--color-success` | Success state |
| `--color-warning` | Warning state |
| `--color-error` | Error state |
| `--radius-selector` | Border radius for selectors |
| `--radius-field` | Border radius for fields |
| `--radius-box` | Border radius for boxes |

## 6. Common Component Patterns

### 6.1 Card with Actions

```html
<div class="card bg-base-100 shadow-xl">
  <figure><img src="..." alt="..." /></figure>
  <div class="card-body">
    <h2 class="card-title">Title</h2>
    <p>Description text</p>
    <div class="card-actions justify-end">
      <button class="btn btn-primary">Action</button>
    </div>
  </div>
</div>
```

### 6.2 Modal

```html
<button class="btn" onclick="my_modal.showModal()">Open</button>
<dialog id="my_modal" class="modal">
  <div class="modal-box">
    <h3 class="text-lg font-bold">Title</h3>
    <p class="py-4">Content</p>
    <div class="modal-action">
      <form method="dialog">
        <button class="btn">Close</button>
      </form>
    </div>
  </div>
  <form method="dialog" class="modal-backdrop">
    <button>close</button>
  </form>
</dialog>
```

### 6.3 Navbar

```html
<div class="navbar bg-base-100">
  <div class="flex-1">
    <a class="btn btn-ghost text-xl">Brand</a>
  </div>
  <div class="flex-none">
    <ul class="menu menu-horizontal px-1">
      <li><a>Link 1</a></li>
      <li><a>Link 2</a></li>
    </ul>
  </div>
</div>
```

### 6.4 Form Group

```html
<div class="form-control w-full max-w-xs">
  <label class="label">
    <span class="label-text">Email</span>
  </label>
  <input type="email" placeholder="email@example.com" class="input input-bordered w-full max-w-xs" />
  <label class="label">
    <span class="label-text-alt">Helper text</span>
  </label>
</div>
```

### 6.5 Drawer Layout

```html
<div class="drawer lg:drawer-open">
  <input id="drawer" type="checkbox" class="drawer-toggle" />
  <div class="drawer-content">
    <!-- Page content -->
    <label for="drawer" class="btn btn-primary drawer-button lg:hidden">Menu</label>
  </div>
  <div class="drawer-side">
    <label for="drawer" class="drawer-overlay"></label>
    <ul class="menu bg-base-200 text-base-content min-h-full w-80 p-4">
      <li><a>Item 1</a></li>
      <li><a>Item 2</a></li>
    </ul>
  </div>
</div>
```

## 7. Responsive Patterns

DaisyUI classes work with Tailwind's responsive prefixes:

```html
<!-- Small button on mobile, large on desktop -->
<button class="btn btn-sm lg:btn-lg">Responsive</button>

<!-- Stack on mobile, horizontal on desktop -->
<div class="flex flex-col lg:flex-row gap-4">
  <div class="card bg-base-100 shadow">...</div>
  <div class="card bg-base-100 shadow">...</div>
</div>
```

## 8. Combining with Tailwind Utilities

DaisyUI classes and Tailwind utility classes work together:

```html
<button class="btn btn-primary w-full mt-4 shadow-lg">
  Full width primary button with margin and shadow
</button>

<div class="card bg-base-100 shadow-xl max-w-md mx-auto">
  Centered card with max width
</div>
```

## 9. Anti-Patterns

| Don't | Do Instead |
|-------|-----------|
| `class="bg-blue-500 text-white px-4 py-2 rounded"` for buttons | `class="btn btn-primary"` |
| Manually define color schemes | Use `data-theme` and CSS variables |
| Hard-code colors like `bg-blue-500` for themed elements | Use `bg-primary`, `bg-secondary`, etc. |
| Mix DaisyUI component classes with conflicting Tailwind utilities | DaisyUI base classes first, then Tailwind overrides |
| Create custom CSS for standard components | Check DaisyUI component library first |

## 10. Workflow Summary

| Step | Action |
|------|--------|
| 1. Identify component | What UI element is needed? |
| 2. Check reference | `get_component(framework: "daisyui", ..., variant: "button")` |
| 3. Use base class | Apply the component's base class |
| 4. Add modifiers | Color, size, style modifiers as needed |
| 5. Add Tailwind | Layer Tailwind utilities for spacing, layout |
| 6. Theme | Set `data-theme` or define custom theme variables |