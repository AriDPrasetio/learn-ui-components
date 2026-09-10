# 🗺️ PROJECT ROADMAP

> Roadmap lengkap dari foundation hingga seluruh 20 komponen selesai.
> Gunakan dokumen ini sebagai panduan harian. Centang item saat selesai.

---

## Konvensi Dokumen Ini

| Simbol  | Arti                              |
| :------ | :-------------------------------- |
| `- [ ]` | Belum dikerjakan                  |
| `- [/]` | Sedang dikerjakan                 |
| `- [x]` | Selesai                           |
| 🔑      | Skill kunci yang dilatih          |
| 🪙      | Token baru yang perlu ditambahkan |
| 📝      | Catatan / reminder                |

---

## 📋 Update Log

- **Revisi audit (2026-09-10)**: tambah `prefers-reduced-motion` override global (M1.6), catatan troubleshooting ES Modules (M1.8), klarifikasi `role="alert"` statis vs dinamis (M2.5), update pola Drag & Drop ke rekomendasi APG terkini (M4.4), opsi matikan autoplay saat reduced-motion (M4.5), opsional automated a11y check (M5). Arsitektur inti (ITCSS, 2-tier token, BEM, tooling) tidak berubah — sudah solid.

---

## Git Workflow Reminder

```text
Setiap milestone / komponen baru:
1. git switch main && git pull origin main
2. git switch -c feat/[nama-branch]
3. Build, lint, commit (atomic)
4. git push origin feat/[nama-branch]
5. Create PR di GitHub → Squash & Merge
6. git switch main && git pull origin main
7. git branch -d feat/[nama-branch]
```

---

## M1: Foundation Scaffold

> **Branch**: `feat/foundation-scaffold`
> **Estimasi**: 2–3 jam
> **🔑 Skills**: ITCSS architecture, 2-tier design tokens, CSS logical properties, semantic HTML

### M1.1 — Folder Structure

- [ ] Buat seluruh folder structure:

  ```text

  css/settings/primitive/
  css/settings/semantic/
  css/generic/
  css/elements/
  css/objects/
  css/utilities/
  js/modules/
  ui/
  assets/fonts/inter/
  assets/images/
  assets/icons/
  ```

### M1.2 — Tooling

- [ ] `npm init -y`
- [ ] Install devDependencies:

  ```bash
  npm install --save-dev stylelint stylelint-config-standard eslint prettier serve
  ```

- [ ] Buat `package.json` dengan scripts (`dev`, `lint:css`, `lint:js`, `format`, `lint`)
- [ ] Buat `.stylelintrc.json`
- [ ] Buat `.eslintrc.json`
- [ ] Buat `.prettierrc`
- [ ] Buat `.gitignore`

### M1.3 — Font Setup

- [ ] Download `Inter-Variable.woff2` dari [GitHub rsms/inter](https://github.com/rsms/inter/releases)
- [ ] Simpan di `assets/fonts/inter/Inter-Variable.woff2`
- [ ] Tambahkan `OFL-Inter.txt` (license file)
- [ ] Buat `css/settings/primitive/fonts.css` dengan `@font-face` declaration

### M1.4 — Primitive Tokens (Minimal Starter)

- [ ] `css/settings/primitive/colors.css` — slate (6 shade) + blue (4 shade)
- [ ] `css/settings/primitive/typography.css` — font family, sizes, weights
- [ ] `css/settings/primitive/spacing.css` — `--space-1` s/d `--space-8`
- [ ] `css/settings/primitive/radii.css` — sm, md, full
- [ ] `css/settings/primitive/shadows.css` — sm, md
- [ ] `css/settings/primitive/motion.css` — fast, normal durations + easing
- [ ] `css/settings/primitive/index.css` — aggregator import

### M1.5 — Semantic Tokens (Minimal Starter)

- [ ] `css/settings/semantic/colors.css` — bg, text, brand, border, focus
- [ ] `css/settings/semantic/typography.css` — font-family-base, font sizes
- [ ] `css/settings/semantic/surfaces.css` — radius, shadow
- [ ] `css/settings/semantic/layout.css` — container max-width, z-index (minimal)
- [ ] `css/settings/semantic/theme-dark.css` — dark mode overrides
- [ ] `css/settings/semantic/index.css` — aggregator import
- [ ] `css/settings/index.css` — imports primitive + semantic

### M1.6 — Base ITCSS Layers

- [ ] `css/generic/reset.css` — modern box-sizing, margin reset, media fluid rules
  - [ ] 🪙 Global `@media (prefers-reduced-motion: reduce)` override — set `animation-duration`/`transition-duration` ke ~0.01ms untuk semua elemen (WCAG 2.1 AA best practice, belum ada di versi sebelumnya)
- [ ] `css/elements/base.css` — body, headings (h1–h3), paragraphs, using semantic tokens
- [ ] `css/elements/links.css` — link styles, `:focus-visible` ring
- [ ] `css/objects/container.css` — `.o-container`, `.o-container--narrow`
- [ ] `css/objects/grid.css` — `.o-stack` (vertical spacing), `.o-cluster` (horizontal), `.o-grid`
- [ ] `css/utilities/u-accessibility.css` — `.u-sr-only`

### M1.7 — Master Orchestrator

- [ ] `css/main.css` — import semua layers dalam urutan ITCSS

### M1.8 — Shared JavaScript

- [ ] `js/modules/utils.js` — `delegate()` function, `onReady()` helper
- [ ] `js/modules/theme-toggle.js` — dark/light mode switcher
- [ ] `js/main.js` — entry point, import modules

📝 **Catatan troubleshooting ES Modules**: topik ini formal baru dibahas belakangan di roadmap JS Fase 2 — kalau stuck di sini, cek 3 hal ini dulu sebelum menyimpulkan "belum paham JS":

- `<script type="module" src="js/main.js">` di HTML — lupa `type="module"` menyebabkan `Uncaught SyntaxError: Cannot use import statement outside a module`
- Path import harus eksplisit relatif dan menyertakan ekstensi (`./utils.js`, bukan `utils`)
- Native ES Modules butuh HTTP server (`serve`) — tidak akan jalan kalau `index.html` dibuka langsung via `file://`

### M1.9 — Landing Page

- [ ] `index.html` — katalog page dengan:
  - [ ] Font preload `<link>`
  - [ ] Semantic landmarks (`<header>`, `<main>`, `<footer>`)
  - [ ] Link ke `css/main.css`
  - [ ] Heading + deskripsi repo
  - [ ] Grid/list kosong untuk link ke komponen (akan diisi nanti)
  - [ ] Theme toggle button
  - [ ] `<script type="module" src="js/main.js">`

### M1.10 — Documentation

- [ ] `README.md` (English) — project description, architecture overview, how to run
- [ ] `ui/README.md` — panduan cara menambah komponen baru

### M1.11 — Verify & Ship

- [ ] Jalankan `npm run dev` → buka `http://localhost:3000`
- [ ] Pastikan font ter-load (no 404)
- [ ] Pastikan dark mode toggle berfungsi
- [ ] `npm run lint` → no errors
- [ ] Push & PR → Squash & Merge

**Exit Criteria**: `index.html` tampil dengan Inter font, dark mode toggle works, semua linting pass.

---

## M2: Phase 1 — Basic Components (CSS-Only)

> **🔑 Focus**: Semantic HTML, flat BEM naming, semantic tokens, CSS logical properties, `:focus-visible`
> **Estimasi**: 1–2 jam per komponen

📝 _Setiap komponen di bawah ini mengikuti workflow yang sama. Centang setiap sub-item._

---

### M2.1 — Button `feat/01-button`

🔑 BEM modifiers, interactive states, `:focus-visible`

- [ ] Buat folder `ui/01-button/`
- [ ] `index.html` — demo page dengan semua variant dan state
- [ ] `c-button.css`:
  - [ ] `.c-button` base block
  - [ ] Modifiers: `--primary`, `--secondary`, `--ghost`, `--outline`
  - [ ] Size modifiers: `--sm`, `--lg` (opsional)
  - [ ] States: `:hover`, `:focus-visible`, `:active`, `:disabled`
  - [ ] Gunakan semantic tokens exclusively
  - [ ] CSS logical properties only
- [ ] Accessibility:
  - [ ] Gunakan `<button>` (bukan `<div>` atau `<a>`)
  - [ ] `:focus-visible` ring yang visible
  - [ ] `disabled` attribute support
- [ ] `NOTES.md` — catatan belajar (🇮🇩)
- [ ] Update `index.html` katalog — tambahkan link ke Button
- [ ] Lint → Push → PR → Squash & Merge

---

### M2.2 — Badge / Tag `feat/02-badge`

🔑 Inline display, color variants, semantic `<span>`

- [ ] Buat folder `ui/02-badge/`
- [ ] `index.html` — demo page
- [ ] `c-badge.css`:
  - [ ] `.c-badge` base block
  - [ ] Color modifiers: `--info`, `--success`, `--warning`, `--error`
  - [ ] Size modifiers: `--sm` (opsional)
- [ ] 🪙 Token baru yang mungkin dibutuhkan:
  - [ ] Primitive: `--primitive-color-green-*`, `--primitive-color-red-*`, `--primitive-color-amber-*`
  - [ ] Semantic: `--color-feedback-success`, `--color-feedback-error`, `--color-feedback-warning`
- [ ] `NOTES.md`
- [ ] Update katalog → Lint → Push → PR

---

### M2.3 — Card `feat/03-card`

🔑 `<article>`, flex/grid layout, surface tokens

- [ ] Buat folder `ui/03-card/`
- [ ] `index.html` — demo page
- [ ] `c-card.css`:
  - [ ] `.c-card` base (surface, shadow, radius)
  - [ ] Elements: `__image`, `__header`, `__title`, `__body`, `__footer`
  - [ ] Modifier: `--horizontal` (side-by-side layout, opsional)
- [ ] Accessibility:
  - [ ] Gunakan `<article>` sebagai root
  - [ ] Heading hierarchy dalam card
- [ ] `NOTES.md`
- [ ] Update katalog → Lint → Push → PR

---

### M2.4 — Avatar `feat/04-avatar`

🔑 `border-radius: 50%`, `aspect-ratio`, image fallback

- [ ] Buat folder `ui/04-avatar/`
- [ ] `index.html` — demo page
- [ ] `c-avatar.css`:
  - [ ] `.c-avatar` base (circle, sizing)
  - [ ] Size modifiers: `--sm`, `--md`, `--lg`
  - [ ] `__fallback` element (initials when no image)
- [ ] 🪙 Token baru yang mungkin dibutuhkan:
  - [ ] Semantic: `--size-avatar-sm`, `--size-avatar-md`, `--size-avatar-lg` (opsional)
- [ ] `NOTES.md`
- [ ] Update katalog → Lint → Push → PR

---

### M2.5 — Alert / Callout `feat/05-alert`

🔑 `role="alert"`, feedback color variants

- [ ] Buat folder `ui/05-alert/`
- [ ] `index.html` — demo page
- [ ] `c-alert.css`:
  - [ ] `.c-alert` base block
  - [ ] Modifiers: `--info`, `--success`, `--warning`, `--error`
  - [ ] Elements: `__icon`, `__title`, `__message`, `__close`
- [ ] Accessibility:
  - [ ] `role="alert"` **hanya** untuk alert yang di-inject/berubah secara dinamis saat runtime (mis. hasil validasi form) — screen reader tidak akan announce konten yang sudah statis di DOM sejak page load
  - [ ] Untuk callout statis (dokumentasi, catatan info) — cukup semantic HTML tanpa `role="alert"`, atau `role="status"` kalau tetap butuh live region yang lebih halus
  - [ ] Close button dengan `aria-label="Dismiss"`
- [ ] `NOTES.md`
- [ ] Update katalog → Lint → Push → PR

---

**🏁 Phase 1 Exit Criteria**:

- [ ] 5 komponen selesai dan ter-link di katalog
- [ ] Semua menggunakan semantic tokens (zero raw hex)
- [ ] Semua menggunakan CSS logical properties
- [ ] `npm run lint` pass tanpa error
- [ ] Dark mode berfungsi di semua komponen

---

## M3: Phase 2 — Intermediate Components (CSS + JS + ARIA)

> **🔑 Focus**: ARIA attribute management (Method 3), keyboard navigation, event delegation, focus management
> **Estimasi**: 2–4 jam per komponen

📝 _Mulai dari sini, setiap komponen interaktif punya file `.js` tersendiri._

---

### M3.1 — Accordion `feat/06-accordion`

🔑 `aria-expanded`, `aria-controls`, `Enter`/`Space` toggle

- [ ] Buat folder `ui/06-accordion/`
- [ ] `index.html` — demo page (multiple accordion items)
- [ ] `c-accordion.css`:
  - [ ] `.c-accordion`, `__item`, `__trigger`, `__panel`
  - [ ] CSS transition untuk panel open/close
  - [ ] Styling via `[aria-expanded="true"]` attribute selector
- [ ] `accordion.js`:
  - [ ] Toggle `aria-expanded` on click
  - [ ] `aria-controls` linking trigger → panel
  - [ ] Keyboard: `Enter` / `Space` to toggle
  - [ ] Event delegation pattern
- [ ] Accessibility:
  - [ ] `<button>` for triggers (not `<div>`)
  - [ ] `aria-expanded="true/false"`
  - [ ] `aria-controls="panel-id"`
  - [ ] `id` pada setiap panel
- [ ] `NOTES.md`
- [ ] Update katalog → Lint → Push → PR

---

### M3.2 — Tabs `feat/07-tabs`

🔑 `role="tablist"`, `aria-selected`, roving tabindex, arrow keys

- [ ] Buat folder `ui/07-tabs/`
- [ ] `index.html`
- [ ] `c-tabs.css`:
  - [ ] `.c-tabs`, `__list`, `__tab`, `__panel`
  - [ ] Active tab styling via `[aria-selected="true"]`
- [ ] `tabs.js`:
  - [ ] `role="tablist"` on container
  - [ ] `role="tab"` on each tab, `role="tabpanel"` on each panel
  - [ ] `aria-selected="true/false"` toggling
  - [ ] `aria-controls` / `aria-labelledby` linking
  - [ ] Arrow key navigation (Left/Right) with roving `tabindex`
  - [ ] `Home` / `End` key support
- [ ] `NOTES.md`
- [ ] Update katalog → Lint → Push → PR

---

### M3.3 — Modal / Dialog `feat/08-modal`

🔑 `<dialog>`, focus trapping, `Escape` dismiss, `aria-modal`

- [ ] Buat folder `ui/08-modal/`
- [ ] `index.html`
- [ ] `c-modal.css`:
  - [ ] `.c-modal`, `__overlay`, `__content`, `__header`, `__body`, `__footer`, `__close`
  - [ ] Backdrop/overlay styling
- [ ] `modal.js`:
  - [ ] Gunakan `<dialog>` element + `.showModal()` / `.close()`
  - [ ] Focus trap (tab cycling within modal)
  - [ ] `Escape` key to close
  - [ ] Return focus ke trigger element saat close
  - [ ] `aria-modal="true"`, `aria-labelledby`
  - [ ] Prevent body scroll saat modal open
- [ ] `NOTES.md`
- [ ] Update katalog → Lint → Push → PR

---

### M3.4 — Dropdown Menu `feat/09-dropdown`

🔑 `aria-haspopup`, `aria-expanded`, click-outside dismiss

- [ ] Buat folder `ui/09-dropdown/`
- [ ] `index.html`
- [ ] `c-dropdown.css`:
  - [ ] `.c-dropdown`, `__trigger`, `__menu`, `__item`
  - [ ] Positioning (absolute relative to trigger)
- [ ] `dropdown.js`:
  - [ ] `aria-haspopup="true"` on trigger
  - [ ] `aria-expanded="true/false"` toggling
  - [ ] Click outside to close
  - [ ] `Escape` to close
  - [ ] Arrow key navigation (Up/Down) within menu items
  - [ ] `role="menu"`, `role="menuitem"`
- [ ] `NOTES.md`
- [ ] Update katalog → Lint → Push → PR

---

### M3.5 — Toast / Notification `feat/10-toast`

🔑 `aria-live="polite"`, auto-dismiss timer, stacking

- [ ] Buat folder `ui/10-toast/`
- [ ] `index.html`
- [ ] `c-toast.css`:
  - [ ] `.c-toast`, `__message`, `__close`
  - [ ] Position fixed, stacking layout
  - [ ] Modifiers: `--success`, `--error`, `--warning`, `--info`
  - [ ] Entry/exit animations
- [ ] `toast.js`:
  - [ ] Toast container with `aria-live="polite"`
  - [ ] `role="status"`
  - [ ] Auto-dismiss with configurable timeout
  - [ ] Manual dismiss via close button
  - [ ] Stack multiple toasts
- [ ] `NOTES.md`
- [ ] Update katalog → Lint → Push → PR

---

### M3.6 — Tooltip `feat/11-tooltip`

🔑 `aria-describedby`, positioning, hover + focus trigger

- [ ] Buat folder `ui/11-tooltip/`
- [ ] `index.html`
- [ ] `c-tooltip.css`:
  - [ ] `.c-tooltip`, `__content`
  - [ ] Position variants: top, bottom, left, right
  - [ ] Arrow/caret styling
- [ ] `tooltip.js`:
  - [ ] Show on `:hover` AND `:focus` (dual trigger)
  - [ ] `aria-describedby` linking trigger → tooltip content
  - [ ] `role="tooltip"` on content
  - [ ] `Escape` to dismiss
  - [ ] Delay sebelum show (prevent flicker)
- [ ] `NOTES.md`
- [ ] Update katalog → Lint → Push → PR

---

### M3.7 — Responsive Navbar `feat/12-navbar`

🔑 Hamburger toggle, mobile menu, responsive breakpoints

- [ ] Buat folder `ui/12-navbar/`
- [ ] `index.html`
- [ ] `c-navbar.css`:
  - [ ] `.c-navbar`, `__brand`, `__toggle`, `__menu`, `__item`, `__link`
  - [ ] Desktop: horizontal menu
  - [ ] Mobile: hamburger + collapsible vertical menu
  - [ ] Mobile-first `@media (min-width: ...)`
- [ ] `navbar.js`:
  - [ ] Hamburger `aria-expanded` toggling
  - [ ] `aria-controls` linking toggle → menu
  - [ ] `aria-label="Main navigation"` on `<nav>`
  - [ ] Close menu on `Escape`
  - [ ] Close menu on resize to desktop
- [ ] 🪙 Token baru yang mungkin dibutuhkan:
  - [ ] Semantic: `--breakpoint-md`, `--z-index-navbar`
- [ ] `NOTES.md`
- [ ] Update katalog → Lint → Push → PR

---

**🏁 Phase 2 Exit Criteria**:

- [ ] 7 komponen interaktif selesai dan ter-link di katalog
- [ ] Semua komponen keyboard-navigable (Tab, Enter, Space, Escape, Arrow)
- [ ] ARIA attributes benar dan sinkron dengan visual state
- [ ] Method 3 pattern digunakan (CSS reads ARIA, JS toggles ARIA)
- [ ] Dark mode berfungsi di semua komponen
- [ ] `npm run lint` pass

---

## M4: Phase 3 — Advanced Components

> **🔑 Focus**: Complex keyboard patterns, data handling, advanced ARIA roles, performance
> **Estimasi**: 4–8 jam per komponen

📝 _Komponen di fase ini jauh lebih kompleks. Tidak harus dikerjakan berurutan — pilih yang paling menarik atau relevan._

---

### M4.1 — Autocomplete / Combobox `feat/13-autocomplete`

🔑 `role="combobox"`, `aria-activedescendant`, debounce, filtering

- [ ] `ui/13-autocomplete/`
- [ ] `index.html`, `c-autocomplete.css`, `autocomplete.js`
- [ ] ARIA: `role="combobox"`, `aria-autocomplete="list"`, `aria-activedescendant`, `aria-expanded`, `role="listbox"`, `role="option"`
- [ ] Keyboard: Arrow Up/Down navigate options, Enter selects, Escape closes
- [ ] Debounced input filtering
- [ ] `NOTES.md` → Lint → Push → PR

### M4.2 — Data Table `feat/14-data-table`

🔑 Sortable columns, `aria-sort`, `<th scope>`, responsive

- [ ] `ui/14-data-table/`
- [ ] `index.html`, `c-data-table.css`, `data-table.js`
- [ ] Semantic: `<table>`, `<thead>`, `<tbody>`, `<th scope="col">`, `<caption>`
- [ ] Sortable headers with `aria-sort="ascending/descending/none"`
- [ ] Responsive pattern (horizontal scroll or card-stack on mobile)
- [ ] `NOTES.md` → Lint → Push → PR

### M4.3 — Date Picker `feat/15-date-picker`

🔑 `role="grid"`, arrow key grid navigation, date logic

- [ ] `ui/15-date-picker/`
- [ ] `index.html`, `c-date-picker.css`, `date-picker.js`
- [ ] Calendar grid with `role="grid"`, `role="gridcell"`
- [ ] Arrow key navigation (up/down/left/right = week/day)
- [ ] Month/year navigation
- [ ] `aria-selected`, `aria-current="date"`
- [ ] `NOTES.md` → Lint → Push → PR

### M4.4 — Drag & Drop List `feat/16-drag-drop`

🔑 `aria-grabbed`, pointer events, reorder logic

- [ ] `ui/16-drag-drop/`
- [ ] `index.html`, `c-drag-drop.css`, `drag-drop.js`
- [ ] Pointer/mouse event handling for drag
- [ ] Visual drop indicator
- [ ] 📝 `aria-grabbed`/`aria-dropeffect` sudah dihapus dari spec ARIA 1.2 — boleh dicoba untuk nilai edukasi, tapi implementasi utama pakai pola APG terkini di bawah
- [ ] Keyboard alternative: select + move item dengan arrow keys, umumkan hasil reorder via `aria-live="polite"`
- [ ] `NOTES.md` → Lint → Push → PR

### M4.5 — Carousel / Slider `feat/17-carousel`

🔑 `aria-roledescription`, `aria-live`, swipe gestures

- [ ] `ui/17-carousel/`
- [ ] `index.html`, `c-carousel.css`, `carousel.js`
- [ ] `aria-roledescription="carousel"`, `aria-label`
- [ ] `aria-live="polite"` for slide announcements
- [ ] Prev/Next buttons, dot indicators
- [ ] Swipe gesture support (touch events)
- [ ] Pause auto-play on hover/focus
- [ ] Matikan auto-play sepenuhnya jika `prefers-reduced-motion: reduce` terdeteksi
- [ ] `NOTES.md` → Lint → Push → PR

### M4.6 — Multi-Select / Chips `feat/18-multi-select`

🔑 `role="listbox"`, `aria-multiselectable`, chip removal

- [ ] `ui/18-multi-select/`
- [ ] `index.html`, `c-multi-select.css`, `multi-select.js`
- [ ] `role="listbox"`, `aria-multiselectable="true"`
- [ ] Chip creation on select, removal on click/Backspace
- [ ] Keyboard: Arrow navigate, Space toggle, Backspace remove last chip
- [ ] `NOTES.md` → Lint → Push → PR

### M4.7 — Tree View `feat/19-tree-view`

🔑 `role="tree"`, `role="treeitem"`, recursive expand/collapse

- [ ] `ui/19-tree-view/`
- [ ] `index.html`, `c-tree-view.css`, `tree-view.js`
- [ ] `role="tree"`, `role="treeitem"`, `role="group"` for nested
- [ ] `aria-expanded` on parent nodes
- [ ] Arrow key navigation: Right (expand), Left (collapse/parent), Up/Down (prev/next)
- [ ] `NOTES.md` → Lint → Push → PR

### M4.8 — Command Palette `feat/20-command-palette`

🔑 Fuzzy search, keyboard-only navigation, `role="combobox"`

- [ ] `ui/20-command-palette/`
- [ ] `index.html`, `c-command-palette.css`, `command-palette.js`
- [ ] Open with `Ctrl+K` / `Cmd+K`
- [ ] `role="combobox"` + `role="listbox"` pattern
- [ ] Fuzzy text matching/filtering
- [ ] Keyboard-only navigation
- [ ] Group/section results
- [ ] `NOTES.md` → Lint → Push → PR

---

**🏁 Phase 3 Exit Criteria**:

- [ ] Semua komponen advanced yang dipilih selesai
- [ ] Complex keyboard patterns berfungsi
- [ ] Semua ARIA roles dan states sesuai WAI-ARIA Authoring Practices
- [ ] `npm run lint` pass

---

## M5: Polish & Publish

> **Branch**: `feat/polish-and-publish`
> **Estimasi**: 2–3 jam

- [ ] **Quality Audit**:
  - [ ] Jalankan Lighthouse di setiap halaman — target score ≥ 95
  - [ ] Cek semua keyboard navigation end-to-end
  - [ ] Cek color contrast di light AND dark mode
  - [ ] Responsive test: 320px, 768px, 1024px, 1440px
  - [ ] (Opsional) Jalankan axe DevTools / `axe-core` per komponen sebagai automated a11y check tambahan di luar Lighthouse
- [ ] **Katalog page (`index.html`)**:
  - [ ] Semua 20 komponen ter-link dengan thumbnail/preview
  - [ ] Komponen dikelompokkan per phase (Basic / Intermediate / Advanced)
  - [ ] Search/filter komponen (opsional, bisa jadi komponen ke-21 😄)
- [ ] **README.md Final**:
  - [ ] Project description
  - [ ] Screenshot / GIF preview
  - [ ] Architecture overview (ITCSS + 2-tier tokens)
  - [ ] How to run locally
  - [ ] Component list with links
  - [ ] Tech stack & standards (WCAG 2.1 AA, BEM, etc.)
  - [ ] License
- [ ] **Deploy ke GitHub Pages**:
  - [ ] Enable GitHub Pages (Settings → Pages → Source: main / root)
  - [ ] Verifikasi live URL berfungsi
- [ ] Push → PR → Squash & Merge

**Exit Criteria**: Repo publik, deployed, documented, dan bisa di-showcase.

---

## 🪙 Token Growth Tracker

Gunakan tabel ini untuk tracking token baru yang ditambahkan seiring komponen berkembang.

| Komponen   | Token Baru yang Ditambahkan                                                                               |
| :--------- | :-------------------------------------------------------------------------------------------------------- |
| Foundation | Slate, blue, spacing 1–8, base typography, radii, shadows, motion                                         |
| Button     | _(kemungkinan tidak perlu token baru)_                                                                    |
| Badge      | `--primitive-color-red-*`, `--primitive-color-green-*`, `--primitive-color-amber-*`, `--color-feedback-*` |
| Card       | _(kemungkinan tidak perlu token baru)_                                                                    |
| Avatar     | _(size tokens opsional)_                                                                                  |
| Alert      | _(reuse feedback tokens dari Badge)_                                                                      |
| Accordion  | _(kemungkinan motion token)_                                                                              |
| Modal      | `--z-index-modal`, `--color-bg-overlay`                                                                   |
| Navbar     | `--breakpoint-md`, `--z-index-navbar`                                                                     |
| Toast      | `--z-index-toast`                                                                                         |
| ...        | _isi saat komponen dikerjakan_                                                                            |

---

## 📊 Progress Summary

| Phase                      |    Total    | Selesai | Progress      |
| :------------------------- | :---------: | :-----: | :------------ |
| M1: Foundation             | 11 sections |    0    | ░░░░░░░░░░ 0% |
| M2: Basic (Phase 1)        | 5 komponen  |    0    | ░░░░░░░░░░ 0% |
| M3: Intermediate (Phase 2) | 7 komponen  |    0    | ░░░░░░░░░░ 0% |
| M4: Advanced (Phase 3)     | 8 komponen  |    0    | ░░░░░░░░░░ 0% |
| M5: Polish & Publish       | 4 sections  |    0    | ░░░░░░░░░░ 0% |

---

> 💡 **Tips**: Jangan terburu-buru menyelesaikan semua. Kualitas > kuantitas.
> Satu komponen yang benar-benar dipahami lebih berharga dari 10 komponen yang di-copy-paste.
> Tulis `NOTES.md` dengan jujur — itu catatan belajarmu yang paling berharga.
