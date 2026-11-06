# YK Collection

A fashion store built for a Nigerian seller who takes orders on WhatsApp. Shoppers browse a proper catalogue, build a cart and send the order to WhatsApp in one tap. The owner manages products from a login-protected admin panel on their phone.

**Live site:** https://yk-collection-2-0.vercel.app/

## Why I built it

Many fashion sellers in Nigeria sell through WhatsApp chats and status updates, with no catalogue. Customers scroll for photos, ask for prices and sizes, and orders get lost. YK Collection puts the products, sizes, stock and reviews in one place and keeps WhatsApp as the checkout, because that is how customers already pay and talk to the seller.

## Features

**For shoppers**
- Browse by category (clothing, shoes, bags, watches, jewelry, jerseys), with search, sorting and filters by size
- Product pages with a photo gallery, full-screen zoom (pinch on a phone), size picker, stock status and an optional 360° spin view
- Reviews and star ratings
- Cart saved on the shopper's own device, with **WhatsApp checkout**: the order is sent as a ready-written message
- Shareable links to a single product
- Feedback and complaint forms, and a "join our WhatsApp list" button
- Light and dark theme

**For the owner (admin panel)**
- Hidden login: tap the footer text five times, then sign in
- Add, edit and delete products, with several photos per product picked straight from the phone gallery (each photo is shrunk to about 300 KB before upload)
- Mark items sold out, mark categories as "coming soon", delete reviews, read customer feedback

## Tech

| Part | Used |
|---|---|
| Front end | HTML, CSS and vanilla JavaScript (no framework, no build step) |
| Database, login, photo storage | [Supabase](https://supabase.com) (Postgres, Auth, Storage) |
| Hosting | Vercel, deployed from this repo |

## How the data is protected

The site talks to Supabase straight from the browser, so the database enforces who can do what with **Row Level Security** (see `supabase-schema.sql`):

| Who | Products | Reviews | Feedback | Photos |
|---|---|---|---|---|
| Any visitor | read | read and post | send only | view |
| Admin | add, edit, delete | also delete | read and delete | upload and delete |

Only user ids listed in the `admins` table count as admin. The key in `supabase-config.js` is a *publishable* key, which is designed to be public. No secret or `service_role` key is used anywhere in this repo.

## Run it yourself

It is a plain static site, so there is nothing to install.

1. Create a free Supabase project and follow **[SETUP.md](SETUP.md)**. It covers the SQL, the admin user, the photo bucket and the keys.
2. Put your project URL and publishable key in `supabase-config.js`.
3. Serve the folder, for example:
   ```bash
   python3 -m http.server 3000
   ```
   then open http://localhost:3000.

## Files

| File | What it does |
|---|---|
| `index.html`, `styles.css` | The page and its styling |
| `script.js` | Storefront: catalogue, filters, cart, WhatsApp checkout, reviews, galleries |
| `admin.js` | Admin panel: login, photo upload, product and category management |
| `supabase-config.js` | Project URL and publishable key |
| `supabase-schema.sql` | Tables, security rules and the photo bucket |
| `supabase-additions.css` | Styles for the photo picker |
| `SETUP.md` | Step-by-step Supabase setup |

## Credits

Designed and built by Kidddarts (Augustine Ucheaga). Contact: augustineucheaga@gmail.com
