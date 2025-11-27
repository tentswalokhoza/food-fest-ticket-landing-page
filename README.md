# cooking-masterclass-catalogue

Simple Vue 3 + Vite catalogue prototype for the "Cooking Masterclass" project.

Overview
- Single-page app that displays a catalogue of cooking workshops.
- Users can save courses to a wishlist and see the wishlist count in the header.

Features
- Course cards rendered from local data (no API)
- 'Sold Out' badge for unavailable classes
- Save/unsave to wishlist with counter in the header
- Responsive grid layout

Run locally
1. Install dependencies

```powershell
npm install
```

2. Start dev server

```powershell
npm run dev
```

3. Build for production

```powershell
npm run build
```

Notes
- Project files are under `src/`.
- Main components added: `src/components/CourseCard.vue`, `src/components/HeaderWishlist.vue`.
- This repository is intended to be renamed to `cooking-masterclass-catalogue` before publishing.

If you'd like, I can add a screenshot file and polish styles further (animations, filters, etc.).
