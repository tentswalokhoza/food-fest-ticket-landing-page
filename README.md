# food-fest-ticket-landing-page

Cape Town Food Fest — Ticket landing page built with Vue 3 + Vite.

Overview
- Single-page landing displaying ticket tiers (Bronze, Silver, Gold).
- Users can favourite tiers and see the wishlist count in the header.

Features
- Ticket cards rendered from local data (no API)
- Featured tier (Gold) is visually highlighted
- Favourite (save) interaction with header count
- Responsive layout for mobile and desktop

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
- Main components: `src/components/CourseCard.vue`, `src/components/HeaderWishlist.vue`.
- Images are in `public/images`.

If you want, I can add a screenshot file and polish interactions (animations, persistence, or CTA buttons).
