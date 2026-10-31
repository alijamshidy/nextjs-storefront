# Next.js Storefront

A **modern E-Commerce Storefront** built with **Next.js 16, Prisma 7, PostgreSQL, Clerk Authentication, and Stripe**. Full-stack in a single app: products are served via server actions (no external API), payments run through Stripe Embedded Checkout, and product images are managed on Cloudinary.

> ℹ️ The package name is `store`.

---

## ✨ Features

### 🛒 **Shopping**
- Product catalog with text search (debounced, matches product name/company) and grid/list layout toggle
- Product details page
- Shopping cart with persistence (per signed-in user, stored in PostgreSQL)
- Wishlist / favorites
- Product reviews and ratings from customers

### 👤 **Authentication ([Clerk](https://clerk.com/))**
- Sign-in / sign-up via **Clerk modal components** (there are no dedicated `/sign-in` or `/sign-up` pages)
- All routes except `/`, `/products`, and `/about` require sign-in (enforced in [`proxy.ts`](proxy.ts) — Next.js 16's renamed middleware)
- **Admin access** is granted to the single Clerk user whose ID matches the `ADMIN_USER_ID` env var (enforced in the middleware and again server-side in `utils/actions.ts`)

### 💳 **Checkout & Payment ([Stripe](https://stripe.com/))**
- Single-step **Stripe Embedded Checkout**
- Confirmation via Stripe's `return_url` redirect to `GET /api/confirm?session_id=...` (no webhook)
- Order history — a table of paid orders

### 📦 **Product Management (Admin)**
- Product CRUD with a single Cloudinary-hosted image per product
- Product creation form with **faker-based autofill** (dev helper) for quick demo data
- Admin pages: products (create/list), orders, and sales (orders table with totals)

### 🎨 **UI/UX**
- Responsive, mobile-first design
- Dark/light mode via [next-themes](https://github.com/pacocoursey/next-themes)
- shadcn/ui-style components on [Radix UI](https://www.radix-ui.com/) primitives

---

## 🛠 Tech Stack

- [Next.js 16](https://nextjs.org/) (App Router) + [React 18](https://react.dev/) + [TypeScript](https://www.typescriptlang.org/)
- [Prisma 7](https://www.prisma.io/) + [PostgreSQL](https://www.postgresql.org/) — via `@prisma/adapter-pg` (driver adapter + `pg` Pool); models: `Product`, `Favorite`, `Review`, `Cart`, `CartItem`, `Order` (users exist only as `clerkId` strings — there is no User model)
- [@clerk/nextjs](https://clerk.com/) — authentication
- [Stripe](https://stripe.com/) — payments (server-side SDK + Embedded Checkout)
- [Cloudinary](https://cloudinary.com/) — product image hosting
- [Tailwind CSS](https://tailwindcss.com/) — styling
- Data access via **server actions** in `utils/actions.ts` and the Prisma singleton in `utils/db.ts`
- [@faker-js/faker](https://fakerjs.dev/) — dev-only form autofill

---

## 💻 Installation

### Prerequisites
- **Node.js 20.9+** (required by Next.js 16)
- npm
- A **PostgreSQL** database
- A [Clerk](https://clerk.com/) account (keys + an admin user ID)
- A [Stripe](https://stripe.com/) account (test keys are fine)
- A [Cloudinary](https://cloudinary.com/) account (for product images)

### Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/alijamshidy/nextjs-storefront.git
   cd nextjs-storefront
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Set up environment variables:**
   ```bash
   cp .env.example .env
   ```
   > ⚠️ Use a file named **`.env`** (not `.env.local`): [`prisma.config.ts`](prisma.config.ts) loads the environment with `dotenv/config`, which reads `.env` only. Next.js reads `.env` too, so a single file works for both.

4. **Set up the database:**
   ```bash
   npx prisma db push     # create the schema (no migrations are committed)
   npx prisma generate    # generate the client (also runs automatically on `npm run build`)
   npx prisma db seed     # seed 4 demo products from prisma/products.json
   ```

5. **Run the development server:**
   ```bash
   npm run dev
   ```

6. **Build for production:**
   ```bash
   npm run build
   npm run start
   ```

The application will start at `http://localhost:3000`.

---

## ⚙ Environment Variables

All variables are in [`.env.example`](.env.example):

| Variable | Description |
|----------|-------------|
| `DATABASE_URL` | PostgreSQL connection string (**required**) |
| `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY` | Clerk publishable key |
| `CLERK_SECRET_KEY` | Clerk secret key |
| `ADMIN_USER_ID` | Clerk user ID of the admin (unlocks `/admin`) |
| `STRIPE_SECRET_KEY` | Stripe secret key (server-side checkout) |
| `NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY` | Stripe publishable key |
| `CLOUDINARY_NAME` | Cloudinary cloud name |
| `CLOUDINARY_KEY` | Cloudinary API key |
| `CLOUDINARY_SECRET` | Cloudinary API secret |
| `NEXT_PUBLIC_WEBSITE_URL` | Public site URL (used by the share button) |
| `KEEP_ALIVE_TOKEN` | Token required by `GET /api/keep-alive?token=...` (returns 403 otherwise) |

---

## 📡 API Routes

| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| POST | `/api/payment` | Signed-in | Creates a Stripe Checkout session for the cart |
| GET | `/api/confirm` | Public | Stripe `return_url` — verifies the session and marks the order paid |
| GET | `/api/keep-alive` | Token-protected | Health check / DB keep-alive (`?token=` must match `KEEP_ALIVE_TOKEN`) |

Everything else (products, cart, favorites, reviews, orders) goes through **server actions**, not HTTP endpoints.

---

## 📁 Folder Structure

```
nextjs-storefront/
├── app/
│   ├── page.tsx             # Homepage (featured products)
│   ├── products/            # Catalog + [id] details page
│   ├── cart/                # Cart page
│   ├── checkout/            # Stripe Embedded Checkout
│   ├── favorites/           # Wishlist
│   ├── orders/              # Order history
│   ├── reviews/             # Customer reviews ([productId])
│   ├── admin/               # Admin area (Sidebar, products create/list, orders, sales)
│   ├── about/               # About page
│   ├── api/                 # payment, confirm, keep-alive routes
│   ├── providers.tsx / theme-provider.tsx
│   └── layout.tsx
├── components/              # home/, products/, single-product/, cart/, checkout/,
│                            # favorites/, reviews/, admin/, navbar/, form/, ui/
├── prisma/
│   ├── schema.prisma        # Product, Favorite, Review, Cart, CartItem, Order
│   ├── products.json        # Seed data (4 demo products)
│   └── seed.js
├── utils/
│   ├── actions.ts           # Server actions (products, cart, favorites, reviews, orders)
│   ├── db.ts                # Prisma singleton (driver adapter + pg Pool)
│   └── ...
├── proxy.ts                 # Next.js 16 middleware — route protection + admin gate
├── prisma.config.ts         # Prisma 7 config (loads .env)
└── .env.example
```

---

## 📦 Available Scripts

| Script | Description |
|--------|-------------|
| `npm run dev` | Start development server |
| `npm run build` | Generate Prisma client + build for production |
| `npm run start` | Start production server |
| `npm run lint` | Run ESLint |

Seed command: `npx prisma db seed` (no dedicated npm script).

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📜 License

This project is **private** and all rights are reserved.

---

## 🆘 Support

For support, please open an issue or contact the maintainer.

---

## 🏷 Topics

`nextjs`, `react`, `typescript`, `ecommerce`, `storefront`, `prisma`, `postgresql`, `clerk`, `stripe`, `cloudinary`, `tailwindcss`, `server-actions`
