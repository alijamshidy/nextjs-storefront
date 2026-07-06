# Next.js Storefront

A **modern E-Commerce Storefront** built with **Next.js 14, Prisma, Clerk Authentication, and PostgreSQL**. This application provides a complete online shopping experience with product catalogs, shopping cart, checkout, user authentication, and admin panel.

---

## 📸 Screenshot
*(Add your storefront screenshots here - homepage, product listings, cart, checkout, etc.)*

---

## ✨ Features

### 🛒 **Shopping Features**
- Product catalog with categories and filtering
- Product search with autocomplete
- Shopping cart with persistence
- Wishlist/favorites functionality
- Quick view and product comparison
- Product reviews and ratings

### 👤 **User Authentication**
- Secure authentication with [Clerk](https://clerk.com/)
- Email/password login
- Social login (Google, GitHub, etc.)
- Passwordless login
- User profile management

### 💳 **Checkout & Payment**
- Multi-step checkout process
- Shipping address management
- Payment gateway integration (Stripe)
- Order confirmation and tracking
- Order history

### 📦 **Product Management**
- Product CRUD operations
- Product images and gallery
- Stock management
- Pricing and discounts
- Product variants (size, color, etc.)

### 📊 **Admin Dashboard**
- Product management (CRUD)
- Order management
- User management
- Sales analytics and reports
- Category and collection management

### 🎨 **UI/UX Features**
- Responsive design (mobile-first)
- Dark/light mode support
- Smooth animations and transitions
- Accessibility compliant (WCAG)
- SEO optimized

---

## 🛠 Tech Stack

**Frontend Framework:**
- [Next.js 14](https://nextjs.org/) - React framework with App Router
- [React 18](https://react.dev/) - UI library
- [TypeScript](https://www.typescriptlang.org/) - Type-safe JavaScript

**Authentication:**
- [Clerk](https://clerk.com/) - Complete authentication solution
  - `@clerk/nextjs` - Next.js integration

**Database & ORM:**
- [PostgreSQL](https://www.postgresql.org/) - Relational database
- [Prisma](https://www.prisma.io/) - Next-generation ORM
  - `@prisma/client` - Prisma client
  - `@prisma/adapter-pg` - PostgreSQL adapter

**Styling:**
- [Tailwind CSS](https://tailwindcss.com/) - Utility-first CSS framework
- [next-themes](https://github.com/pacocoursey/next-themes) - Dark/light mode support
- [Radix UI](https://www.radix-ui.com/) - Accessible UI primitives
  - `@radix-ui/react-checkbox`
  - `@radix-ui/react-dropdown-menu`
  - `@radix-ui/react-icons`

**State Management:**
- React Context API
- [Zustand](https://github.com/pmndrs/zustand) (if used)

**Form Handling:**
- [React Hook Form](https://react-hook-form.com/) (if used)
- [Zod](https://zod.dev/) - Schema validation (if used)

**Payment:**
- [Stripe](https://stripe.com/) - Payment processing

**Build Tools:**
- [ESLint](https://eslint.org/) - Code linting
- [Prettier](https://prettier.io/) - Code formatting

---

## 💻 Installation

### Prerequisites
- Node.js (v18 or later)
- npm or yarn
- PostgreSQL database
- Git
- Clerk account (for authentication)
- Stripe account (for payments)

### Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/alijamshidy/nextjs-storefront.git
   cd nextjs-storefront
   ```

2. **Install dependencies:**
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Set up environment variables:**
   ```bash
   cp .env.example .env.local
   ```
   Edit `.env.local` file with your configuration (see [Environment Variables](#-environment-variables))

4. **Set up database:**
   ```bash
   npx prisma generate
   npx prisma migrate dev
   npx prisma db seed
   ```

5. **Run the development server:**
   ```bash
   npm run dev
   # or
   yarn dev
   ```

6. **Build for production:**
   ```bash
   npm run build
   npm run start
   ```

The application will start at `http://localhost:3000`

---

## ⚙ Environment Variables

Create a `.env.local` file in the root directory and add the following variables:

```env
# Next.js Configuration
NEXT_PUBLIC_SITE_URL=http://localhost:3000
NEXT_PUBLIC_API_URL=http://localhost:3000/api

# Clerk Authentication
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
CLERK_SECRET_KEY=your_clerk_secret_key
NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up
NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL=/
NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL=/

# Database (PostgreSQL)
DATABASE_URL=postgresql://username:password@localhost:5432/storefront_db?schema=public

# Stripe Payment
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=your_stripe_publishable_key
STRIPE_SECRET_KEY=your_stripe_secret_key
STRIPE_WEBHOOK_SECRET=your_stripe_webhook_secret

# Cloud Storage (Optional)
NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

# Analytics (Optional)
NEXT_PUBLIC_GOOGLE_ANALYTICS_ID=your_ga_id
```

---

## 📁 Folder Structure

```
nextjs-storefront/
├── app/                      # Next.js App Router
│   ├── about/               # About page
│   ├── admin/               # Admin dashboard
│   │   ├── layout.tsx
│   │   ├── products/
│   │   │   ├── create/
│   │   │   ├── [id]/
│   │   │   │   └── edit/
│   │   │   └── page.tsx
│   │   └── sales/
│   │       └── page.tsx
│   ├── api/                 # API routes
│   │   ├── confirm/
│   │   │   └── route.ts
│   │   ├── keep-alive/
│   │   │   └── route.ts
│   │   └── payment/
│   │       └── route.ts
│   ├── cart/                # Shopping cart
│   │   └── page.tsx
│   ├── checkout/             # Checkout process
│   │   ├── CheckoutClient.tsx
│   │   └── page.tsx
│   ├── favorites/           # Wishlist
│   │   └── page.tsx
│   ├── orders/              # User orders
│   │   └── page.tsx
│   ├── products/            # Product pages
│   │   └── page.tsx
│   ├── reviews/             # Product reviews
│   │   └── page.tsx
│   ├── layout.tsx           # Root layout
│   └── page.tsx             # Homepage
├── components/              # React components
│   ├── cart/                # Cart components
│   ├── form/                # Form components
│   ├── global/              # Global/Shared components
│   ├── home/                # Home page components
│   ├── navbar/              # Navigation components
│   ├── products/            # Product components
│   ├── reviews/             # Review components
│   ├── single-product/      # Single product page components
│   └── ui/                  # UI primitives
├── lib/                     # Utility libraries
├── prisma/                  # Prisma ORM
│   ├── products.json       # Product data (seed)
│   ├── schema.prisma        # Database schema
│   └── seed.js              # Database seeding script
├── public/                  # Static assets
│   └── images/
├── utils/                   # Utility functions
├── components.json
├── eslint.config.mjs
├── .env.example
├── .gitignore
├── package.json
└── README.md
```

---

## 🚀 Demo

### Run the application locally:
```bash
npm run dev
```

### Access the application:
- **Storefront:** `http://localhost:3000`
- **Admin Dashboard:** `http://localhost:3000/admin`
- **Sign In:** `http://localhost:3000/sign-in`
- **Sign Up:** `http://localhost:3000/sign-up`

### Test Accounts (create via Clerk):
- **Admin:** admin@demo.com
- **Customer:** customer@demo.com

---

## 📡 API Documentation

### Base URL
```
http://localhost:3000/api
```

### Authentication Endpoints

| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| GET | `/api/auth` | Get authentication status | Public |

### Payment Endpoints

| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| POST | `/api/payment` | Create payment intent | Private |
| POST | `/api/confirm` | Confirm payment | Private |

### Keep-Alive Endpoint

| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| GET | `/api/keep-alive` | Health check endpoint | Public |

---

## 📦 Available Scripts

| Script | Description |
|--------|-------------|
| `npm run dev` | Start development server |
| `npm run build` | Build for production |
| `npm run start` | Start production server |
| `npm run lint` | Run ESLint |
| `npm run lint:fix` | Fix ESLint issues |
| `npm run type-check` | Run TypeScript type checking |
| `npm run prisma:generate` | Generate Prisma client |
| `npm run prisma:migrate` | Run database migrations |
| `npm run prisma:studio` | Open Prisma Studio |
| `npm run prisma:seed` | Seed database with initial data |

---

## 🎯 Project Roadmap

- [x] Core e-commerce functionality
- [x] User authentication with Clerk
- [x] Product catalog and management
- [x] Shopping cart and checkout
- [x] Admin dashboard
- [ ] Advanced search and filtering
- [ ] Product recommendations
- [ ] Multi-language support
- [ ] Mobile app integration

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

`nextjs`, `react`, `typescript`, `ecommerce`, `prisma`, `postgresql`, `clerk-authentication`, `stripe`, `tailwindcss`, `frontend`, `storefront`, `shopping-cart`, `checkout`, `admin-dashboard`