# 🛍️ Shopify Custom Sections

> Custom Liquid sections built on the Dawn theme — zero dependencies, vanilla JS only.

![Shopify](https://img.shields.io/badge/Platform-Shopify-7AB55C?style=flat-square&logo=shopify&logoColor=white)
![Dawn](https://img.shields.io/badge/Theme-Dawn-000000?style=flat-square)
![Vanilla JS](https://img.shields.io/badge/JavaScript-Vanilla%20ES5-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![No jQuery](https://img.shields.io/badge/jQuery-Not%20Used-red?style=flat-square)

---

## 📂 Sections

All files live in the `sections/` folder and are searchable in the Shopify Theme Editor.

| File | Theme Editor Name | Description |
|------|-------------------|-------------|
| `custom-announcement-bar.liquid` | Custom Announcement Bar | Responsive bar with hamburger toggle |
| `static-announcement-bar.liquid` | Static Announcement Bar | Simple text bar with mobile variant |
| `gift-guide-hero.liquid` | Gift Guide Hero | Banner + content/image split layout |
| `custom-featured-products.liquid` | Custom Featured Products | 6-card lookbook grid with hotspots |
| `custom-product-modal.liquid` | Custom Product Modal | Quick-view popup with Add to Cart |

---

## 🗂️ Project Structure

```
├── sections/
│   ├── custom-announcement-bar.liquid   ✨
│   ├── static-announcement-bar.liquid   ✨
│   ├── gift-guide-hero.liquid           ✨
│   ├── custom-featured-products.liquid  ✨
│   └── custom-product-modal.liquid      ✨
├── assets/
├── config/
├── snippets/
└── templates/
```

---

## ⚙️ Tech Stack

| Layer | Technology |
|-------|------------|
| Platform | Shopify Online Store 2.0 |
| Theme | Dawn |
| Templating | Liquid |
| Styling | Scoped CSS + Custom Properties |
| JavaScript | Vanilla JS (ES5) |
| Cart | Shopify AJAX API (`/cart/add.js`) |

---

## ✨ Features

- ✅ Fully responsive — Desktop → Tablet → Mobile
- ✅ All content editable via Theme Customiser (no code changes needed)
- ✅ Functional Add to Cart with variant matching
- ✅ Auto-add rule: selecting **Black + Medium** also adds *Soft Winter Jacket*
- ✅ Dynamic colour/size detection from product options
- ✅ Swipe-fill button hover animations with `::before`
- ✅ Hamburger toggle on mobile with smooth expand/collapse
- ✅ Separate desktop/mobile text & images
- ✅ Zero external dependencies

---

## 🔄 Add to Cart Flow

```
Click hotspot (+)
    │
    ▼
Modal opens → reads product data from card attributes
    │
    ▼
User selects Colour + Size
    │
    ▼
Click [ADD TO CART]
    │
    ├── Validate selections
    ├── Match variant ID
    └── Black + Medium? → fetch & add Soft Winter Jacket too
    │
    ▼
POST /cart/add.js
    ├── ✅ Success → "✓ ADDED!"
    └── ❌ Error   → "FAILED" → retry
```

---

## 📱 Responsive Breakpoints

| Breakpoint | Grid | Notes |
|------------|------|-------|
| `> 768px` | 3 columns | Full desktop layout |
| `≤ 768px` | 2 columns | Hamburger menu, mobile text |
| `≤ 480px` | 2 columns | Smaller fonts, tighter spacing |

---

## 🧠 Notable Solutions

<details>
<summary><strong>Button text disappearing on hover</strong></summary>

Text was a bare text node — can't receive `z-index`. Wrapped in `<span>` so the `::before` swipe-fill no longer covers it.

```html
<button><span class="btn-label">SHOP NOW</span></button>
```
</details>

<details>
<summary><strong>Inline styles overriding CSS variables</strong></summary>

`!important` lost to inline `style="color:..."`. Removed inline styles and switched to a CSS variable:

```css
.btn:hover { color: var(--btn-hover-text); }
```
</details>

<details>
<summary><strong>SVG breaking JSON schema</strong></summary>

Double quotes in SVG conflicted with JSON string delimiters. Converted `"` → `'` and used `currentColor`:

```json
"default": "<svg viewBox='0 0 24 24' fill='currentColor'>...</svg>"
```
</details>

<details>
<summary><strong>Variant matching for cart</strong></summary>

Stored variants as JSON in `data-product-variants`. JS searches `option1/2/3` with priority: exact → colour only → size only → first available.
</details>

<details>
<summary><strong>Auto-add (Black + Medium rule)</strong></summary>

Schema product picker selects the auto-add item. JS checks the colour + size match, fetches via `/products/{handle}.js`, then adds both items in a single `POST /cart/add.js`.
</details>

---

## 🚀 Setup

```bash
# Clone the repo
git clone https://github.com/your-username/your-repo.git

# Create a development branch
git checkout -b development

# Stage, commit, and push
git add .
git commit -m "Add custom sections"
git push origin development
```

Then open a **Pull Request**: `development → master` and connect the branch to your Shopify store.

### Adding a Section to a Page

1. Open **Theme Customiser**
2. Click **Add Section**
3. Search by section name (e.g. *Custom Announcement Bar*)
4. Configure settings → **Save**

---

## 📚 Key Concepts Used

- **Section architecture** — each file is self-contained (HTML + CSS + JS + Schema)
- **Scoped styles** via `#shopify-section-{{ section.id }}`
- **CSS Custom Properties** bridge Liquid settings → CSS
- **IIFE pattern** for JS scope isolation
- **Event delegation** for dynamically rendered elements
- **Fetch API** for cart operations

---

<p align="center">Built with ☕ and vanilla JavaScript · No jQuery was harmed.</p>
