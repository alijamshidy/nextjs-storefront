# Next.js Storefront

A full-stack storefront built with Next.js, TypeScript, Prisma, Clerk, Stripe, Cloudinary, and Tailwind CSS. It includes a customer shopping experience, admin product management, cart and checkout flows, favorites, orders, reviews, and image uploads.

## Screenshot

Add screenshots to `docs/screenshots/` and update the links below:

```md
![Home page](docs/screenshots/home.png)
![Product page](docs/screenshots/product.png)
![Admin products](docs/screenshots/admin-products.png)
```

## Features

- Product catalog with grid/list views
- Product detail pages with ratings, reviews, and sharing
- Cart, checkout, and order confirmation flows
- Favorites and user-specific shopping actions
- Clerk authentication and protected routes
- Admin dashboard for product and sales management
- Stripe payment integration
- Cloudinary image upload/delete helpers
- Prisma database layer with seed data
- Dark mode support and reusable UI components

## Tech Stack

- Next.js 16
- React 18
- TypeScript
- Tailwind CSS 4
- Prisma 7
- PostgreSQL
- Clerk
- Stripe
- Cloudinary
- Radix UI
- shadcn-style components

## Installation

Clone the repository:

```bash
git clone https://github.com/alijamshidy/nextjs-storefront.git
cd nextjs-storefront
```

Install dependencies:

```bash
npm install
```

Create `.env.local`:

```bash
cp .env.example .env.local
```

Generate Prisma client and seed the database if needed:

```bash
npx prisma generate
npx prisma db push
npm run seed
```

Start the development server:

```bash
npm run dev
```

Open `http://localhost:3000`.

## Environment Variables

Create `.env.local` with these values:

```env
DATABASE_URL=

NEXT_PUBLIC_WEBSITE_URL=http://localhost:3000
KEEP_ALIVE_TOKEN=

NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=
ADMIN_USER_ID=

STRIPE_SECRET_KEY=
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=

CLOUDINARY_NAME=
CLOUDINARY_KEY=
CLOUDINARY_SECRET=
```

## Folder Structure

```text
.
├── app/
│   ├── admin/
│   ├── api/
│   ├── cart/
│   ├── checkout/
│   ├── orders/
│   └── products/
├── components/
│   ├── cart/
│   ├── form/
│   ├── home/
│   ├── navbar/
│   ├── products/
│   └── ui/
├── lib/
├── prisma/
│   ├── schema.prisma
│   └── seed.js
├── public/
└── utils/
```

## Demo

Live demo: https://next-js-fullstack-storefront.vercel.app

## Repository Metadata

Suggested description:

```text
Full-stack Next.js storefront with Prisma, Clerk, Stripe, Cloudinary, cart, checkout, reviews, and admin product management.
```

Suggested topics:

```text
nextjs, typescript, ecommerce, storefront, prisma, postgresql, clerk, stripe, cloudinary, tailwindcss
```
