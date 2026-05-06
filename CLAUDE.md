# Araitea Cat's — Design System & Frontend Guidelines

## Project Overview

Static multi-page site for Araitea Cat's, a premium Persian cat breeder in Mexico.
Stack: plain HTML + Tailwind CSS (CDN), no build step.
Each page lives in its own folder (`/venta-de-gatos-persas-en-*/index.html`).

---

## Color Palette

| Token       | Hex       | Usage                                                     |
|-------------|-----------|-----------------------------------------------------------|
| `navy`      | `#0A2241` | Primary background, navbar, section fills, footer         |
| `gold`      | `#CCA052` | Accent: CTAs, dividers, icon highlights, hover states     |
| `gold-light`| `#E2C07E` | Gold tint for subtle backgrounds or disabled states       |
| `cream`     | `#FAF7F2` | Off-white page background, card fills                     |
| `white`     | `#FFFFFF` | Text on dark surfaces, icon fills                         |
| `charcoal`  | `#2D2D2D` | Body copy on light backgrounds                            |
| `mist`      | `#E8E3DB` | Borders, horizontal rules, light dividers                 |

### Tailwind config (applied in every `<script>` block):
```js
tailwind.config = {
  theme: {
    extend: {
      colors: {
        navy:       '#0A2241',
        gold:       '#CCA052',
        'gold-light': '#E2C07E',
        cream:      '#FAF7F2',
        charcoal:   '#2D2D2D',
        mist:       '#E8E3DB',
        whatsapp:   '#25D366',
      },
      fontFamily: {
        serif: ['"Cormorant Garamond"', 'serif'],
        sans:  ['"Josefin Sans"', 'sans-serif'],
      },
    },
  },
};
```

---

## Typography

### Font Loading (Google Fonts — place in every `<head>`)
```html
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link
  href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,500;1,500&family=Josefin+Sans:wght@400;500&display=swap"
  rel="stylesheet"
/>
```

### Scale

| Role              | Class pattern                                              | Notes                                          |
|-------------------|------------------------------------------------------------|------------------------------------------------|
| Display / Hero    | `font-sans text-5xl md:text-7xl font-medium leading-tight` | Josefin Sans Medium, sentence case             |
| Section Title     | `font-sans text-3xl md:text-4xl font-medium`               | Josefin Sans Medium                            |
| Card Title        | `font-sans text-xl font-medium`                            | Josefin Sans Medium                            |
| Gold inline span  | `font-serif italic text-gold`                              | Cormorant Garamond italic — only inside p/h tags |
| Nav Links         | `font-sans text-xs font-medium uppercase tracking-widest`  | Josefin Sans, ALL CAPS, letter-spacing wide    |
| Body / Paragraph  | `font-sans text-base font-normal leading-relaxed`          | Josefin Sans Regular                           |
| Label / Caption   | `font-sans text-sm font-medium`                            | Josefin Sans Medium                            |
| Button Text       | `font-sans text-sm font-medium uppercase tracking-wide`    | Josefin Sans Medium, ALL CAPS                  |

**Font rules:**
- `font-sans` (Josefin Sans) is the default for **all** text — UI, body, headings, labels, buttons.
- `font-serif` (Cormorant Garamond italic) is used **only** on `<span class="text-gold font-serif italic">` inline within `<p>` or `<h1>`–`<h6>` to highlight a gold word or phrase.
- Max font-weight is `font-medium` (500). Never use `font-medium`, `font-medium`, or heavier.

---

## Spacing & Layout

### Base unit: 4px (`1` in Tailwind)

| Step | Value  | Usage                                    |
|------|--------|------------------------------------------|
| 2    | 8px    | Tight inline gaps (icon + label)         |
| 4    | 16px   | Card internal padding                    |
| 6    | 24px   | Section internal spacing                 |
| 8    | 32px   | Component gaps                           |
| 12   | 48px   | Section padding (mobile)                 |
| 16   | 64px   | Section padding (desktop)                |
| 24   | 96px   | Large section separators                 |

### Grid

- **Content max-width:** `max-w-6xl mx-auto px-4 md:px-8`
- **Standard grid:** `grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8`
- **Two-column feature:** `grid grid-cols-1 lg:grid-cols-2 gap-12 items-center`
- **No full-bleed content:** all readable text lives inside the `max-w-6xl` container.

---

## Components

### Navbar

```html
<nav class="bg-navy py-4 px-6 md:px-12 sticky top-0 z-50 shadow-md">
  <div class="max-w-6xl mx-auto flex items-center justify-between">
    <!-- Logo -->
    <a href="/" class="flex items-center gap-3">
      <img src="/assets/logo.svg" alt="Araitea Cat's" class="h-10 w-auto" />
    </a>
    <!-- Links -->
    <ul class="hidden md:flex items-center gap-8">
      <li><a href="/" class="font-sans text-xs font-medium uppercase tracking-widest text-white hover:text-gold transition-colors">Inicio</a></li>
      <li><a href="/venta-de-gatos-persas-en-cdmx/" class="font-sans text-xs font-medium uppercase tracking-widest text-white hover:text-gold transition-colors">CDMX</a></li>
      <!-- repeat per page -->
    </ul>
    <!-- CTA -->
    <a href="https://wa.me/..." class="btn-gold hidden md:inline-flex">Contáctanos</a>
  </div>
</nav>
```

- Background: `bg-navy`
- Active link: `text-gold border-b border-gold pb-0.5`
- Hover: `hover:text-gold transition-colors duration-200`

---

### Buttons

**Primary (Gold CTA)**
```html
<a class="inline-flex items-center gap-2 bg-gold hover:bg-gold-light text-navy font-sans text-sm font-medium uppercase tracking-wide px-6 py-3 rounded-none transition-colors duration-200">
  Ver Gatitos Disponibles
</a>
```

**Secondary (Outlined)**
```html
<a class="inline-flex items-center gap-2 border border-gold text-gold hover:bg-gold hover:text-navy font-sans text-sm font-medium uppercase tracking-wide px-6 py-3 rounded-none transition-colors duration-200">
  Conoce el Criadero
</a>
```

**WhatsApp**
```html
<a class="inline-flex items-center gap-2 bg-whatsapp hover:opacity-90 text-white font-sans text-sm font-medium uppercase tracking-wide px-6 py-3 rounded-none transition-opacity duration-200">
  <!-- WhatsApp SVG icon -->
  Escribir por WhatsApp
</a>
```

**Rules:**
- `rounded-none` — sharp corners reinforce the premium, structured aesthetic.
- Never use `rounded-full` on primary CTAs.
- All button text is ALL CAPS (`uppercase`) via Tailwind class, never in HTML markup.

---

### Cards

```html
<div class="bg-white border border-mist hover:border-gold transition-colors duration-300 p-6 group">
  <!-- optional top accent -->
  <div class="h-0.5 w-12 bg-gold mb-4"></div>
  <h3 class="font-sans text-xl font-medium text-navy mb-2">Título de Tarjeta</h3>
  <p class="font-sans text-base text-charcoal leading-relaxed">Descripción breve.</p>
</div>
```

- Background: `bg-white` on `cream` page backgrounds; `bg-cream` on `white`/`navy` section backgrounds.
- Hover: border transitions to gold (`hover:border-gold`).
- No box shadows on cards — borders do the heavy lifting.

---

### Dividers & Accents

Gold rule under section titles:
```html
<div class="h-0.5 w-16 bg-gold mt-3 mb-8"></div>
```

Section heading pattern (dark background):
```html
<div class="text-center mb-12">
  <p class="font-sans text-xs font-medium uppercase tracking-widest text-gold mb-2">Subtítulo de Categoría</p>
  <h2 class="font-sans text-4xl font-medium text-white">Título Principal</h2>
  <div class="h-0.5 w-16 bg-gold mx-auto mt-4"></div>
</div>
```

Section heading pattern (light background):
```html
<div class="mb-10">
  <p class="font-sans text-xs font-medium uppercase tracking-widest text-gold mb-2">Subtítulo</p>
  <h2 class="font-sans text-4xl font-medium text-navy">Título Principal</h2>
  <div class="h-0.5 w-16 bg-gold mt-4"></div>
</div>
```

---

### Footer

Three-column layout on desktop, stacked on mobile. Background: `bg-navy`. Top gold rule separates footer from page body.

```html
<footer class="bg-navy border-t-2 border-gold">
  <div class="max-w-6xl mx-auto px-6 md:px-8 py-16 grid grid-cols-1 md:grid-cols-3 gap-12">

    <!-- Col 1: Brand -->
    <div>
      <img src="/assets/logo.svg" alt="Araitea Cat's" class="h-10 mb-4" />
      <p class="font-sans text-sm text-white/70 leading-relaxed max-w-xs">
        Criadero de gatos persas con más de 25 años de experiencia. Gatitos libres de PKD.
      </p>
      <div class="h-0.5 w-10 bg-gold mt-6"></div>
    </div>

    <!-- Col 2: Navigation -->
    <div>
      <h4 class="font-sans text-xs font-medium uppercase tracking-widest text-gold mb-5">Navegación</h4>
      <ul class="space-y-3">
        <li><a href="/" class="font-sans text-sm text-white/70 hover:text-gold transition-colors">Inicio</a></li>
        <li><a href="/venta-de-gatos-persas-en-cdmx/" class="font-sans text-sm text-white/70 hover:text-gold transition-colors">Gatos en CDMX</a></li>
        <li><a href="/venta-de-gatos-persas-en-jalisco/" class="font-sans text-sm text-white/70 hover:text-gold transition-colors">Gatos en Jalisco</a></li>
        <li><a href="/venta-de-gatos-persas-en-monterrey/" class="font-sans text-sm text-white/70 hover:text-gold transition-colors">Gatos en Monterrey</a></li>
      </ul>
    </div>

    <!-- Col 3: Contact -->
    <div>
      <h4 class="font-sans text-xs font-medium uppercase tracking-widest text-gold mb-5">Contacto</h4>
      <ul class="space-y-3">
        <li>
          <a href="https://wa.me/..." class="inline-flex items-center gap-2 font-sans text-sm text-white/70 hover:text-gold transition-colors">
            <!-- WhatsApp icon 16x16 -->
            WhatsApp
          </a>
        </li>
        <li>
          <a href="https://instagram.com/..." class="inline-flex items-center gap-2 font-sans text-sm text-white/70 hover:text-gold transition-colors">
            <!-- Instagram icon 16x16 -->
            Instagram
          </a>
        </li>
      </ul>
    </div>

  </div>

  <!-- Bottom bar -->
  <div class="border-t border-white/10 py-4 text-center">
    <p class="font-sans text-xs text-white/40">
      &copy; 2026 Araitea Cat's · Todos los derechos reservados
    </p>
  </div>
</footer>
```

---

## Page Section Cadence

Every page should follow this rhythm to maintain consistency:

1. **Navbar** — `bg-navy`, sticky
2. **Hero** — full-viewport, dark overlay on image, serif headline + gold CTA
3. **Trust strip** — `bg-cream`, 3–4 icon stats (PKD-free, years experience, etc.)
4. **Content section** — alternating `bg-white` / `bg-cream` panels
5. **CTA Band** — `bg-navy`, centered serif heading, gold primary button
6. **Footer** — `bg-navy`, three-column

---

## Do's and Don'ts

**Do:**
- Use `bg-navy` for sections that need weight and authority.
- Use gold sparingly — it works because it's rare. One gold CTA per viewport.
- Keep all nav and button text ALL CAPS via `uppercase` Tailwind class.
- Use `rounded-none` on all interactive elements to maintain the structured feel.
- Use `transition-colors duration-200` on all hover states.
- Prefer `text-white/70` for secondary text on dark backgrounds over pure `text-gray-*`.

**Don't:**
- Use `font-serif` (Cormorant Garamond) anywhere other than inline gold `<span>` inside `<p>` or `<h1>`–`<h6>`.
- Use rounded corners (`rounded-lg`, `rounded-full`) on buttons or cards.
- Use the old brand blue (`#0081C2`) — it has been retired in favor of navy + gold.
- Add drop shadows to cards — use border treatments instead.
- Place body copy wider than `max-w-2xl` — readability degrades.
- Use sentence-case for navigation items — always ALL CAPS.
