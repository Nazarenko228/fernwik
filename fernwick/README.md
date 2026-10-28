# Fernwick — Plant Shop Ecommerce HTML Template

A free, dependency-free **ecommerce template for a plant shop**. Six pages, static HTML,
two stylesheets and one script. No framework, no build step, no jQuery — and a **working
basket** that survives a page reload.

Built for html.design.

---

## Layout spine — shop first

Most ecommerce templates open with a marketing hero and make you scroll to reach a
product. Fernwick opens the way a real shop does:

1. **Announcement bar** — the delivery threshold, stated once
2. **Utility header** — search, account, basket with a live count
3. **Category rail** — horizontally scrollable, snap-aligned
4. **Product grid, immediately** — no hero image on the page at all
5. Dark nursery band → easy-care row → care guides → trust strip

## Pages

| File | What it demonstrates |
|---|---|
| `index.html` | Category rail, two product grids, dark editorial band, care-guide cards, trust strip |
| `shop.html` | Filter sidebar, quick-filter chips, live result count, sorting, and an empty state |
| `product.html` | Gallery with thumbnails, pot-size variants that change the price, quantity stepper, care spec table, accordions, related products |
| `cart.html` | Line items with steppers and remove, order summary, delivery threshold, promo field |
| `care.html` | Editorial guide index with a featured dark article |
| `about.html` | Nursery story, facts table, principles band, visit details and an enquiry form |

## The basket actually works

`assets/js/main.js` keeps the basket in `localStorage`, so it survives refreshes and
navigation between pages. It handles add, quantity change, remove, the free-delivery
threshold (£40), and renders into both the slide-out drawer and the cart page from the
same state.

**Prices are integers in pence** throughout — no float ever touches a total, so you can
never end up with £41.999999. Formatting happens once, at display time.

```js
Fernwick.addItem({
  id: 'monstera', name: 'Monstera Deliciosa',
  price: 4200,              // pence
  image: '…', variant: '17cm pot', qty: 1
});
```

There is no payment backend. Checkout raises a toast — that is where you wire in Stripe,
Shopify, Snipcart or your own handler.

## Filtering and sorting

The shop page filters on data attributes rendered onto each card (`data-tags`,
`data-price`, `data-name`, `data-order`). Chips and checkboxes combine with AND logic,
the result count is live, and an empty state appears when a combination has no matches.
Sorting reorders the existing DOM nodes rather than re-rendering.

## Design direction

- **Colour** — green is the *ink*, not the accent. A pale glasshouse ground `#edf1ea`,
  deep forest text `#14251a`, and a single brass ochre `#c9861f` doing the pointing.
  Red, amber and green appear only as shop state: sale, low stock, in stock.
- **Type** — Epilogue for headings, Be Vietnam Pro for reading, Sometype Mono for labels
  and prices. Prices use tabular figures so columns line up down a grid.
- **Photography** — every plant is shot on a plain ground, which is what makes a mixed
  grid read as one shop rather than a scrapbook.

## Files

```
fernwick/
├── index.html  shop.html  product.html
├── cart.html   care.html  about.html
├── assets/
│   ├── css/  tokens.css · shop.css
│   ├── js/   main.js
│   └── img/  CREDITS.md
└── README.md
```

`tokens.css` holds the design tokens, reset, buttons and form controls. `shop.css` holds
the store chrome — header, rail, product cards, filters, PDP, drawer, footer.

## Customising

Everything visual is a CSS custom property at the top of `assets/css/tokens.css`:

```css
:root {
  --glass:  #edf1ea;   /* page ground   */
  --forest: #14251a;   /* ink           */
  --ochre:  #c9861f;   /* the accent    */
  --sale: #b4462b;  --stock: #3d6b4a;  --low: #a8720d;
}
```

Change `--ochre` and every call to action, focus ring, active state and link follows.

To change the delivery threshold, edit the one comparison in `main.js` (`sub >= 4000`)
and the announcement bar text.

## Accessibility

- Real `<dl>` markup for the care specification, semantic landmarks throughout
- Accordions use `aria-expanded` / `aria-controls`; variants and chips use `aria-pressed`
- The basket count is hidden from assistive tech when empty rather than announcing "0"
- Quick-add is revealed on hover but is always visible on touch devices
- Focus rings are visible; icon-only buttons carry `aria-label`
- Full `prefers-reduced-motion` support

## Browser support

Modern evergreen browsers. Uses `color-mix()` for the sticky header tint and
`aspect-ratio` for the product tiles.

## Notes

- Photography loads from Unsplash at request time — see `assets/img/CREDITS.md`.
  Self-host before production.
- Product copy, prices and care data are illustrative. Replace them with your own.

---

**Name check (informal, not a legal opinion)** — "Fernwick"

- Google: no company, shop or brand under this name; nearest matches are Fenwick
  (a US law firm — different spelling, unrelated class) and Fernished, Inc. (furniture leasing)
- USPTO: no record returned for the exact mark
- Domain: no owner found for fernwick.com
- Rejected during the search: **Verdling** (an active organic baby-products brand),
  **Sylvara** (an active silk homeware brand)
- Verdict: clear to ship
