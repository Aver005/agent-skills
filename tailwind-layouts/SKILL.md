---
name: tailwind-layouts
description: Use when building page layouts, application shells, navigation structures, or responsive page templates with Tailwind CSS. Covers sidebar layouts, stacked layouts, multi-column layouts, dashboard shells, containers, grid systems, responsive breakpoint strategies, sticky headers, fixed sidebars, off-canvas navigation, breadcrumbs, pagination, vertical navigation, content reflow patterns.
---

# Tailwind Layouts

## 1. Application Shell Patterns

| Shell Type | Structure | Key Classes | Best For |
|------------|-----------|-------------|----------|
| Sidebar | Fixed sidebar + scrollable main | `flex min-h-screen` with `fixed inset-y-0 w-72` sidebar + `pl-72 flex-1` main | Admin dashboards, SaaS apps |
| Stacked | Top nav + main content area | `flex flex-col min-h-screen` with sticky nav + `flex-1` main | Marketing sites, simple apps |
| Multi-column | Sidebar + main + secondary panel | `flex min-h-screen` with fixed sidebar + `flex-1` center + `w-80` right panel | Email clients, detail views |
| Full-width stacked | Full-bleed nav + constrained content | Nav spans full width, content inside `max-w-7xl mx-auto` | Content-heavy sites |
| Narrow sidebar | Icon-only sidebar + main | `w-16` sidebar with tooltips, expands on hover or click | Dense tool UIs |

### Responsive Shell Behavior

| Breakpoint | Sidebar Shell | Stacked Shell |
|------------|---------------|---------------|
| Mobile (`<lg`) | Sidebar hidden; off-canvas Dialog triggered by hamburger | Nav collapses to hamburger menu |
| Desktop (`lg+`) | Sidebar visible; main offset with `lg:pl-72` | Full horizontal nav visible |

### Shell Skeleton

```html
<!-- Sidebar shell -->
<div>
  <!-- Mobile sidebar: Dialog with Transition (hidden on lg+) -->
  <!-- Desktop sidebar: fixed inset-y-0 left-0 z-50 w-72 (hidden below lg) -->
  <div class="lg:pl-72">
    <!-- Top bar / header -->
    <main class="py-10"><div class="px-4 sm:px-6 lg:px-8">...</div></main>
  </div>
</div>
```

## 2. Sidebar Patterns

### Sidebar Variants

| Variant | Key Classes | Behavior |
|---------|-------------|----------|
| Fixed light | `fixed inset-y-0 left-0 z-50 w-72 bg-white border-r border-gray-200` | Always visible on desktop |
| Fixed dark | `fixed inset-y-0 left-0 z-50 w-72 bg-gray-900` | Dark background, light text |
| Collapsible | `w-72` expanded / `w-16` collapsed, controlled by state | Toggle between full and icon-only |
| With secondary nav | Primary nav left + nested sub-nav panel | Two-level navigation |
| With expandable sections | Headless UI `Disclosure` for grouped nav items | Accordion-style nav groups |

### Desktop Sidebar Structure

| Element | Classes | Purpose |
|---------|---------|---------|
| Container | `fixed inset-y-0 left-0 z-50 w-72 hidden lg:flex lg:flex-col` | Fixed positioning, hidden on mobile |
| Inner wrapper | `flex grow flex-col gap-y-5 overflow-y-auto px-6 pb-4` | Scrollable nav content |
| Logo area | `flex h-16 shrink-0 items-center` | Top branding |
| Nav list | `flex flex-1 flex-col` with `<ul role="list">` | Semantic navigation |
| Active item | `bg-gray-50 text-indigo-600` (light) / `bg-gray-800 text-white` (dark) | Current page indicator |
| Inactive item | `text-gray-700 hover:text-indigo-600 hover:bg-gray-50` | Default state |

### Mobile Sidebar (Off-Canvas Dialog)

| Element | Classes / Component | Purpose |
|---------|---------------------|---------|
| Overlay | `Dialog` with `fixed inset-0 z-50` backdrop | Blocks interaction with main content |
| Backdrop | `Transition` with opacity animation | Dim background |
| Panel | `fixed inset-y-0 left-0 z-50 w-full max-w-xs` or `w-72` | Slide-in sidebar |
| Close button | `absolute top-0 right-0 -mr-12 pt-2` or inside panel | Dismiss sidebar |
| Transition | `translate-x` from `-full` to `0` | Slide animation |

Mobile sidebar must use Headless UI `Dialog` (or equivalent) for accessibility: focus trapping, Escape to close, aria attributes.

### Sidebar Navigation Item States

| State | Light Theme | Dark Theme |
|-------|-------------|------------|
| Active | `bg-gray-50 text-indigo-600 font-semibold` | `bg-gray-800 text-white` |
| Inactive | `text-gray-700 hover:bg-gray-50 hover:text-indigo-600` | `text-gray-400 hover:bg-gray-800 hover:text-white` |
| Icon (active) | `text-indigo-600` | `text-white` |
| Icon (inactive) | `text-gray-400 group-hover:text-indigo-600` | `text-gray-400 group-hover:text-white` |

## 3. Navigation Patterns

### Navigation Types

| Type | Structure | Key Classes | Responsive Behavior |
|------|-----------|-------------|---------------------|
| Top navbar | `nav` with logo + links + actions | `sticky top-0 z-40 bg-white border-b` | Collapse to hamburger below `lg` |
| Sidebar nav | Vertical link list with optional icons | Inside fixed sidebar container | Becomes off-canvas Dialog on mobile |
| Breadcrumbs | `<ol>` with `<li>` items + separators | `flex items-center gap-x-2` | Truncate middle items on mobile |
| Pagination | Page numbers with prev/next buttons | `flex items-center justify-between` | Simplify to prev/next only on mobile |
| Tabs | `role="tablist"` with `role="tab"` buttons | `border-b border-gray-200` tab bar | Horizontal scroll or convert to dropdown |
| Vertical nav | Stacked links in a sidebar or column | `flex flex-col gap-y-1` | Remains vertical; may move to top on mobile |
| Command palette | Search input + filtered results list | `Dialog` with `Combobox`, `fixed inset-0 z-50` | Full-screen overlay on all sizes |

### Breadcrumb Structure

```html
<nav aria-label="Breadcrumb">
  <ol role="list" class="flex items-center gap-x-2">
    <li><a href="/" class="text-gray-500 hover:text-gray-700">Home</a></li>
    <li class="flex items-center gap-x-2">
      <svg class="h-5 w-5 text-gray-300"><!-- chevron --></svg>
      <a href="/section" class="text-gray-500 hover:text-gray-700">Section</a>
    </li>
    <li class="flex items-center gap-x-2">
      <svg class="h-5 w-5 text-gray-300"><!-- chevron --></svg>
      <span class="text-gray-900 font-medium" aria-current="page">Current</span>
    </li>
  </ol>
</nav>
```

### Pagination Structure

| Element | Classes | Notes |
|---------|---------|-------|
| Container | `flex items-center justify-between border-t border-gray-200 px-4 py-3` | Bottom of list |
| Mobile view | `flex flex-1 justify-between sm:hidden` | Prev/Next buttons only |
| Desktop view | `hidden sm:flex sm:flex-1 sm:items-center sm:justify-between` | Full page numbers |
| Active page | `bg-indigo-600 text-white` | Current page indicator |
| Inactive page | `text-gray-900 ring-1 ring-gray-300 hover:bg-gray-50` | Clickable page numbers |
| Results text | `text-sm text-gray-700` | "Showing 1 to 10 of 97 results" |

### Tab Navigation

| Element | Role / Attribute | Classes |
|---------|------------------|---------|
| Tab container | `role="tablist"` | `flex border-b border-gray-200` |
| Tab button | `role="tab"`, `aria-selected`, `aria-controls` | `px-4 py-2 text-sm font-medium` |
| Active tab | `aria-selected="true"` | `border-b-2 border-indigo-500 text-indigo-600` |
| Inactive tab | `aria-selected="false"` | `text-gray-500 hover:text-gray-700 hover:border-gray-300` |
| Tab panel | `role="tabpanel"`, `aria-labelledby` | Content area below tabs |

## 4. Container and Content Patterns

### Container Widths

| Pattern | Classes | Use Case |
|---------|---------|----------|
| Standard constrained | `max-w-7xl mx-auto px-4 sm:px-6 lg:px-8` | Most page content |
| Narrow content | `max-w-3xl mx-auto px-4 sm:px-6 lg:px-8` | Articles, forms |
| Wide content | `max-w-screen-2xl mx-auto px-4 sm:px-6 lg:px-8` | Data-heavy dashboards |
| Full bleed | No max-width constraint | Hero sections, banners |
| Breakout from container | Negative margins + full viewport width | Full-bleed images inside constrained parent |

### Content with Sidebar Offset

| Layout | Approach |
|--------|----------|
| Fixed sidebar + constrained main | Main has `lg:pl-72`, content inside uses `max-w-7xl mx-auto` |
| Sidebar + centered content | `flex-1` main area with `mx-auto max-w-5xl` inside |
| Full-width main with sidebar | `pl-72` on wrapper; content fills available space |

### Responsive Padding Scale

| Breakpoint | Horizontal Padding | Typical Usage |
|------------|-------------------|---------------|
| Default (mobile) | `px-4` (1rem) | Base padding |
| `sm` (640px+) | `sm:px-6` (1.5rem) | Tablet |
| `lg` (1024px+) | `lg:px-8` (2rem) | Desktop |

Always apply the full responsive padding chain: `px-4 sm:px-6 lg:px-8` for consistent spacing across breakpoints.

### Full-Bleed Breakout Pattern

When content lives inside a constrained container but a section needs to go full width:

```html
<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
  <!-- Constrained content above -->
  <div class="relative left-1/2 right-1/2 -mx-[50vw] w-screen bg-gray-900 py-16">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
      <!-- Full-bleed section content, re-constrained inside -->
    </div>
  </div>
  <!-- Constrained content below -->
</div>
```

### Vertical Spacing Between Sections

| Spacing | Classes | Use Case |
|---------|---------|----------|
| Tight | `py-8 sm:py-12` | Dense dashboard sections |
| Standard | `py-16 sm:py-24` | Marketing page sections |
| Generous | `py-24 sm:py-32` | Hero, major page breaks |

## 5. Grid Patterns

### Grid Types

| Pattern | Classes | Use Case |
|---------|---------|----------|
| Responsive columns | `grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6` | Card grids, feature sections |
| Four-column | `grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-4 gap-6` | Dashboard stat cards |
| Auto-fit | `grid gap-6` with inline `grid-template-columns: repeat(auto-fit, minmax(min(18rem, 100%), 1fr))` | Self-adjusting card grids |
| Two-column asymmetric | `grid grid-cols-1 lg:grid-cols-[1fr_280px] gap-8` or `lg:grid-cols-3` with `lg:col-span-2` + `lg:col-span-1` | Main + sidebar content |
| Form layout (7/5) | `grid grid-cols-1 lg:grid-cols-12 gap-8` with `lg:col-span-7` + `lg:col-span-5` | Form + preview |
| Form layout (8/4) | Same 12-col grid with `lg:col-span-8` + `lg:col-span-4` | Content + aside |

### Column Spanning

| Utility | Effect |
|---------|--------|
| `col-span-full` | Span all columns (full-width row item) |
| `sm:col-span-2` | Span 2 columns at `sm`+ |
| `lg:col-span-3` | Span 3 columns at `lg`+ |
| `col-start-1 row-start-1` | Place at specific grid position (enables overlapping) |

### Layered Grid (Overlapping Elements)

Place multiple children at the same grid cell using explicit `col-start-1 row-start-1` on each. Later DOM elements render on top. Useful for image overlays, card badges, or transition effects.

### Grid vs Flexbox Decision

| Use Grid When | Use Flexbox When |
|---------------|------------------|
| 2D layout (rows and columns) | 1D layout (single row or column) |
| Equal-sized card grids | Distributing space among items |
| Complex column spanning needed | Simple horizontal nav or toolbar |
| Overlapping elements | Content of unknown/variable size |
| Defined track structure | Items that should wrap naturally |

## 6. Sticky and Fixed Elements

### Positioning Patterns

| Pattern | Classes | Notes |
|---------|---------|-------|
| Sticky header | `sticky top-0 z-40 bg-white/95 backdrop-blur` | Stays at top during scroll |
| Fixed sidebar | `fixed inset-y-0 left-0 z-50 w-72` | Always visible, out of flow |
| Sticky section header | `sticky top-16 z-30 bg-white` | Sticks below main header (`top-16` = header height) |
| Sticky table header | `sticky top-0 z-10 bg-white` on `<thead>` | Table scrolls, header stays |
| Sticky footer | `sticky bottom-0 z-40 bg-white border-t` | Action bar at bottom of viewport |
| Fixed bottom bar | `fixed bottom-0 inset-x-0 z-50` | Mobile action bar |

### z-index Strategy

| Layer | z-index | Usage |
|-------|---------|-------|
| Base content | `z-0` | Default stacking |
| Sticky table headers | `z-10` | Above table rows |
| Dropdowns, tooltips | `z-20` | Above sticky elements |
| Sticky section headers | `z-30` | Above dropdowns |
| Sticky page header | `z-40` | Above section headers |
| Sidebar, off-canvas | `z-50` | Above everything except modals |
| Modal/Dialog backdrop | `z-50` | Full-screen overlay |
| Modal/Dialog content | `z-50` | On top of backdrop (later in DOM) |
| Toast notifications | `z-[60]` | Above modals if needed |

Use Tailwind's default `z-*` scale. Avoid arbitrary values (`z-[999]`) unless layering above third-party elements. Keep z-index assignments consistent across the project.

### Scroll Behavior with Fixed/Sticky Elements

| Scenario | Solution |
|----------|----------|
| Main content scrolls, sidebar fixed | `overflow-y-auto` on main, `fixed` sidebar |
| Both sidebar and main scroll independently | `overflow-y-auto` on both, both `fixed` or within flex container |
| Prevent body scroll when modal open | Add `overflow-hidden` to `<body>` when Dialog is open |
| Smooth scroll to anchor | `scroll-smooth` on `<html>` or `scroll-behavior: smooth` |
| Offset scroll target for sticky header | `scroll-mt-16` on target elements (matches header height) |

## 7. Responsive Layout Strategy

### Mobile-First Approach

Write base styles for mobile, then layer up with breakpoint prefixes. Tailwind breakpoints are `min-width` by default.

| Breakpoint | Prefix | Min Width | Typical Target |
|------------|--------|-----------|----------------|
| Default | (none) | 0px | Mobile phones |
| sm | `sm:` | 640px | Large phones, small tablets |
| md | `md:` | 768px | Tablets |
| lg | `lg:` | 1024px | Small desktops, laptops |
| xl | `xl:` | 1280px | Desktops |
| 2xl | `2xl:` | 1536px | Large desktops |

### Common Responsive Shifts

| Element | Mobile | Desktop |
|---------|--------|---------|
| Sidebar | Hidden; Dialog off-canvas | `fixed inset-y-0 left-0 w-72` visible |
| Top nav links | Hidden; hamburger menu | `hidden lg:flex lg:gap-x-6` visible |
| Grid columns | `grid-cols-1` | `sm:grid-cols-2 lg:grid-cols-3` |
| Stack direction | `flex flex-col` | `lg:flex-row` |
| Padding | `px-4` | `sm:px-6 lg:px-8` |
| Font size | `text-2xl` | `sm:text-3xl lg:text-4xl` |

### Responsive Visibility

| Pattern | Classes | Purpose |
|---------|---------|---------|
| Show on desktop only | `hidden lg:flex` or `hidden lg:block` | Desktop nav, sidebar |
| Show on mobile only | `lg:hidden` | Hamburger button, mobile nav |
| Hide completely | `hidden` | Controlled by JS state |
| Show with flex | `hidden sm:flex` | Flex container at breakpoint |

## 8. Page Section Patterns

### Hero Section

| Element | Classes | Notes |
|---------|---------|-------|
| Container | `relative isolate overflow-hidden` | Background effects contained |
| Inner | `mx-auto max-w-7xl px-4 sm:px-6 lg:px-8 py-24 sm:py-32` | Responsive padding |
| Heading | `text-4xl sm:text-5xl lg:text-6xl font-bold tracking-tight` | Responsive sizing |
| Subheading | `mt-6 text-lg text-gray-600 max-w-2xl` | Constrained width for readability |
| CTA group | `mt-10 flex items-center gap-x-6` | Button row |

### Feature Grid

| Variant | Structure |
|---------|-----------|
| 3-column icon grid | `grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8` with icon + title + description per cell |
| 2-column with image | `grid grid-cols-1 lg:grid-cols-2 gap-12 items-center` with text block + image |
| Alternating rows | Repeat 2-column grid, swap order with `lg:order-first` / `lg:order-last` |

### Split Layout (Text + Image)

| Element | Classes |
|---------|---------|
| Container | `grid grid-cols-1 lg:grid-cols-2 gap-12 items-center` |
| Text column | `max-w-lg` or unconstrained within grid cell |
| Image column | `aspect-[4/3] overflow-hidden rounded-xl` or `aspect-video` |
| Reverse order | Add `lg:order-first` on the image column |

### List/Detail Split View

| Element | Classes | Notes |
|---------|---------|-------|
| Container | `flex min-h-screen` | Full height |
| List panel | `w-96 border-r overflow-y-auto` | Fixed width, scrollable |
| Detail panel | `flex-1 overflow-y-auto` | Fills remaining space |
| Mobile | Show list or detail (not both); use routing or state to toggle | Single-panel view |

### Settings Page with Sidebar Tabs

| Element | Classes |
|---------|---------|
| Container | `grid grid-cols-1 lg:grid-cols-[220px_1fr] gap-8` |
| Tab list | `flex lg:flex-col gap-1` | Horizontal on mobile, vertical on desktop |
| Active tab | `bg-gray-100 text-gray-900 font-medium rounded-md px-3 py-2` |
| Content panel | `min-w-0` (prevents overflow in grid) |

## 9. Common Anti-Patterns

| Anti-Pattern | Problem | Solution |
|--------------|---------|----------|
| Fixed pixel widths (`w-[400px]`) | Breaks on smaller screens | Use responsive classes: `w-full lg:w-96` |
| Missing mobile navigation | Sidebar/nav disappears below breakpoint | Add Dialog-based off-canvas menu for mobile |
| Arbitrary z-index values (`z-[9999]`) | Unpredictable stacking, conflicts | Follow consistent z-index scale (10/20/30/40/50) |
| Sidebar not accessible on mobile | Keyboard/screen reader users cannot navigate | Use Headless UI `Dialog` with focus trapping |
| Content overflow on small screens | Horizontal scroll, clipped text | Use `overflow-hidden`, `truncate`, `min-w-0` on flex/grid children |
| Hardcoded sidebar offset (`ml-72`) | Breaks when sidebar width changes | Use `lg:pl-72` matching sidebar `w-72`; update both together |
| Missing `min-h-screen` on shell | Footer floats mid-page on short content | Add `min-h-screen` to outermost flex container |
| Sticky header without background | Content shows through header on scroll | Add `bg-white` or `bg-white/95 backdrop-blur` |
| Grid without `min-w-0` on children | Long content overflows grid cell | Add `min-w-0` to grid children that may contain long text |
| Inline styles for layout | Inconsistent with utility-first approach | Use Tailwind classes; use arbitrary values `[]` only as last resort |
| Nav without `aria-label` | Poor screen reader experience | Add `aria-label="Main navigation"` or similar to `<nav>` elements |
| Forgetting `isolate` on hero/sections | Background effects bleed into adjacent sections | Add `isolate` to create new stacking context |

## MCP Component Library

The `frontend-components` MCP server provides layout-related components:

- **HyperUI** (`hyperui`): Application layouts (side-menu, vertical-menu, grids, tabs), marketing layouts (headers, footers, sections, banners)
- **DaisyUI** (`daisyui`): Drawer, navbar, footer, hero, dock, divider class references
- **FlyonUI** (`flyonui`): Navbar, drawer, footer CSS components

**Layout search:** `search_components(query: "sidebar", framework: "hyperui")` or `list_components(framework: "hyperui", category: "application")` to browse application layout components.