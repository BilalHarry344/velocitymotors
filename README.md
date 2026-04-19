# Velocity Motors

**Velocity Motors** is a static, multi-page marketing and showroom website for a fictional performance car dealership. It presents a dark, sporty visual identity, mobile-first layouts, and demo content (placeholder cars, Unsplash imagery, and non-functional forms).

---

## What this project is

| Aspect | Description |
|--------|-------------|
| **Purpose** | Showcase inventory-style browsing, a single detailed vehicle page, and contact/about content with a consistent brand experience. |
| **Type** | Plain HTML, CSS, and a small amount of JavaScript. No build step, no package manager, no backend. |
| **Content** | Demonstration copy, sample vehicle names, and stock photos. Not connected to real inventory or APIs. |

---

## Tech stack

| Layer | Technology |
|-------|------------|
| **Markup & layout** | HTML5, [Bootstrap 5.3.3](https://getbootstrap.com/) (grid, navbar, forms, carousel, modal, offcanvas, pagination). |
| **Icons** | [Bootstrap Icons 1.11.3](https://icons.getbootstrap.com/) |
| **Typography** | [Google Fonts — Inter](https://fonts.google.com/specimen/Inter) (weights 400–800). |
| **Custom styling** | `assets/css/theme.css` (design tokens, components, motion). |
| **Behavior** | `assets/js/main.js` (scroll reveal, copyright year, reduced-motion handling). |
| **Images** | [Unsplash](https://unsplash.com/) URLs embedded in HTML. |

All framework and font assets load from public CDNs; an internet connection is required for first load unless you vendor those files locally.

---

## Repository layout

```
velocitymotors/
├── index.html              # Home: hero, stats, featured cars, categories, value props, reviews carousel, footer
├── inventory.html          # Filter sidebar / mobile offcanvas, search & sort UI, car grid, pagination
├── car-detail.html         # Gallery carousel, specs, inquiry form, test-drive modal, similar cars
├── contact.html            # About Velocity, contact details, map placeholder area, contact form
├── assets/
│   ├── css/
│   │   └── theme.css       # Global theme, components, responsive rules
│   └── js/
│       └── main.js         # IntersectionObserver reveals + year injection
└── README.md               # This file
```

---

## Pages (what each file does)

### `index.html` — Home

- Fixed dark navbar with links to all pages and a primary call-to-action.
- Hero with headline, supporting copy, and hero image.
- Stat band (demo numbers).
- **Featured cars**: three cards linking to the shared detail page.
- **Body style** tiles (Sport SUV, Supercars, Luxury Sedan, Electric Performance) linking to inventory.
- **Why choose us** and quick-link tiles (trade-in, EMI, service — narrative only).
- Customer quotes **carousel** (Bootstrap).
- Footer with dynamic copyright year (via `data-current-year`).

### `inventory.html` — Inventory

- Desktop: sticky **filter** panel (brand, fuel, budget — UI only; does not filter data).
- Mobile: same filters in a Bootstrap **offcanvas** drawer.
- Search input and sort `<select>` (presentation only).
- Grid of **six** demo vehicles with badges, specs line, price, and link to `car-detail.html`.
- Pagination controls (static demo).

### `car-detail.html` — Vehicle detail (single template)

- **Image gallery** carousel for one featured model (*Apex Evo X Carbon* — demo).
- Price, model year, mileage, actions: test drive (opens **modal**), financing anchor.
- **Performance specs** grid (power, acceleration, top speed, drive, fuel, warranty).
- Highlights list.
- **`#inquiry`** section: “Get Personalized Offer” form with Bootstrap `needs-validation` / `novalidate` (client-side validation markup only; no submit handler or server).
- **Similar cars** row linking back to the same detail template for comparison CTAs.

### `contact.html` — Contact & about

- About section and three pillar cards (team, delivery, community).
- Fictional address, phone, email, hours.
- Contact / inquiry form (same limitation as car detail: no backend).

---

## `assets/css/theme.css` — design system overview

CSS custom properties under `:root` define the **Velocity “sb” (showroom bold)** palette:

| Token | Role |
|-------|------|
| `--sb-bg`, `--sb-bg-soft` | Page backgrounds |
| `--sb-surface`, `--sb-surface-2` | Cards, panels, inputs |
| `--sb-text`, `--sb-text-muted` | Primary and secondary text |
| `--sb-primary` | Brand red (buttons, accents) |
| `--sb-secondary` | Blue (hovers, feature icons) |
| `--sb-accent` | Orange (gradient with primary) |
| `--sb-border`, `--sb-shadow`, `--sb-radius-*`, `--sb-transition` | Shared chrome |

**Notable utility and component classes**

| Class / pattern | Meaning |
|-----------------|--------|
| `.text-muted-sb` | Muted body text color |
| `.bg-soft-sb` | Soft section background |
| `.surface-sb` | Bordered card/panel surface |
| `.brand-gradient` | Gradient text on “Motors” and headings |
| `.navbar-sb` | Glass-style fixed navbar |
| `.btn-brand` / `.btn-outline-brand` | Primary and outline pill buttons |
| `.badge-sb` | Soft red badge for labels |
| `.card-sb` | Inventory/detail card with hover lift |
| `.tile-card` / `.tile-overlay` | Category image tiles |
| `.stat-item` | Small stat blocks |
| `.feature-icon` | Icon wrapper for feature sections |
| `.footer-sb` | Footer strip |
| `.section-padding`, `.section-title`, `.section-lead` | Vertical rhythm and headings |
| `.hero`, `.hero-card`, `.hero-img`, `.hero-animate` | Home hero layout and entrance animation |
| `.reveal` / `.reveal.in-view` | Scroll-triggered fade/slide-in |
| `.car-gallery-frame` | Detail page gallery height and cropping |

**Accessibility and motion**

- `prefers-reduced-motion: reduce` shortens transitions/animations and keeps `.reveal` visible without motion.
- Form controls use dark surfaces and visible focus rings aligned with `--sb-secondary`.

---

## `assets/js/main.js` — behavior

The script is wrapped in an IIFE and does two things:

1. **Scroll reveal**  
   Elements with class `.reveal` are observed with `IntersectionObserver`. When they enter the viewport, `.in-view` is added (once). If the user prefers reduced motion, all `.reveal` nodes get `.in-view` immediately and no observer runs.

2. **Copyright year**  
   Every element with `[data-current-year]` gets the current calendar year from `new Date().getFullYear()`.

There is no routing, no state management, and no AJAX.

---

## How to run locally

Because the site is static HTML, you only need to open the files in a browser **or** serve the folder so CDN links resolve reliably:

**Option A — open a file**

- Double-click `index.html`, or drag it into a browser.  
- Some browsers restrict `file://` behavior for modules or certain APIs; CDNs should still load.

**Option B — local HTTP server (recommended)**

From the project root:

```bash
python3 -m http.server 8080
```

Then visit `http://localhost:8080/` and navigate between pages.

Other tools (`npx serve`, VS Code Live Server, etc.) work the same way: point the server root at this folder.

---

## Customization checklist

| Goal | Where to look |
|------|----------------|
| Colors, radii, motion | `:root` and components in `assets/css/theme.css` |
| Copy, meta titles, images | Each `.html` file |
| Nav labels and hrefs | Navbar block repeated in each page (keep in sync or extract with a templating tool later) |
| Add real forms | Replace demo `<form>` elements with `action`/`method` or JavaScript that posts to your API |

---

## Limitations (by design)

- **No database**, inventory API, or authentication.
- **Filters, search, sort, pagination, and forms** are visual prototypes only.
- **Contact and phone/email** are fictional (`example` domain, generic address).
- **Images** depend on Unsplash availability and their terms of use.

---

## License

No license file is included in this repository. If you publish or reuse the project, add a `LICENSE` file that matches your intent.
