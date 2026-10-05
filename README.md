# NOVA MART — Simple Ecommerce Store

**CodeAlpha Full Stack Development Internship — Task 1**

A production-style, full-stack e-commerce storefront: **React + Vite + Tailwind CSS** frontend, **Node.js + Express + Prisma + PostgreSQL** backend, JWT authentication, and a fully seeded demo catalogue.

---

## ✨ Features

### Storefront
- Responsive premium UI (mobile → desktop) with product grid, category navigation, and search
- **Product listing** with full-text search, category/price filters, in-stock filter, multiple sorting options
- **Product detail pages** with image gallery, specifications, reviews, and related products
- **Persistent shopping cart** (guest + login merge), quantity controls, remove items
- **Checkout** with full validation → order creation → confirmation page
- **Order history** & order detail view
- **Wishlist** with add, remove, toggle
- **User account** profile management

### Authentication & Security
- Register / login with JWT (`Bearer`), bcrypt password hashing
- **Zod** request validation
- **Helmet** security headers
- **Rate limiting** on authentication and API endpoints
- **CORS** explicit origin allowlist
- Password hashes never exposed in API responses

### Backend
- **REST API** under `/api`, layered architecture (controllers → services → Prisma)
- **PostgreSQL** via Prisma ORM with migrations and demo seed
- Runs with **Docker Postgres** or one-command embedded Postgres (no install required)

---

## 🛠 Tech Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React 19, Vite, Tailwind CSS 3, React Router 7, lucide-react |
| **Backend** | Node.js ≥18, Express 5, Zod validation, JWT, Helmet, express-rate-limit |
| **Database** | PostgreSQL 17 + Prisma ORM (migrations, seed, typed client) |
| **DevOps** | Docker Compose (optional), embedded Postgres fallback |

---

## 📦 Project Structure

```
CodeAlpha_Simple_Ecommerce_Store/
├── backend/
│   ├── prisma/            # Schema, migrations, seed, demo product data
│   ├── scripts/           # Embedded Postgres helper
│   └── src/
│       ├── controllers/   # Request → service → response mapping
│       ├── services/      # Business logic
│       ├── routes/        # /api routers
│       └── server.js      # Express app entry
├── frontend/
│   └── src/
│       ├── pages/         # Home, Shop, Product, Cart, Checkout, Orders, Account
│       ├── components/    # Layout, product cards, cart, UI primitives
│       ├── context/       # Auth, Cart, Wishlist providers
│       └── lib/api.js     # Typed fetch client (envelope-unwrapping)
├── docker-compose.yml     # Optional one-command PostgreSQL
└── package.json           # Workspace scripts
```

---

## 🚀 Getting Started

### 1. Install Dependencies
```bash
npm run install:all
```

### 2. Configure Environment

**backend/.env** (see `backend/.env.example`):
```env
DATABASE_URL="postgresql://nova:nova@localhost:5432/novamart?schema=public"
JWT_SECRET="change-me"
PORT=5000
```

**frontend/.env** (see `frontend/.env.example`):
```env
VITE_API_URL="http://localhost:5000/api"
```

### 3. Start PostgreSQL — Choose One

**Option A — Docker** (requires Docker):
```bash
docker compose up -d
```

**Option B — Embedded Postgres** (zero-config, recommended):
```bash
npm --prefix backend run db:local
```

### 4. Migrate & Seed Database
```bash
npm run db:setup
```

### 5. Run in Development
```bash
# Terminal 1 - Backend (http://localhost:5000)
npm run dev:backend

# Terminal 2 - Frontend (http://localhost:5173)
npm run dev:frontend
```

### Production Build
```bash
npm run build          # outputs frontend/dist
npm --prefix backend start
```

---

## 🔌 API Overview

Base URL: `http://localhost:5000/api`

| Area | Endpoints |
|---|---|
| **Auth** | `POST /auth/register`, `POST /auth/login`, `GET /auth/me`, `PUT /auth/profile`, `PUT /auth/password` |
| **Products** | `GET /products` (search/filter/sort), `GET /products/:slug`, `GET /products/summary`, `GET /categories` |
| **Cart** | `GET /cart`, `POST /cart`, `PATCH /cart/:itemId`, `DELETE /cart/:itemId`, `DELETE /cart`, `POST /cart/merge` |
| **Wishlist** | `GET /wishlist`, `POST /wishlist/:productId` |
| **Orders** | `POST /orders`, `GET /orders`, `GET /orders/:id`, `POST /orders/:id/cancel` |
| **Admin** | `POST/PATCH/DELETE /products…`, `GET/PATCH /admin/orders…` (role-gated server-side) |

Responses follow the envelope: `{ success, data, message? }`

---

## ✅ Quality Assurance

- **60/60 backend integration tests pass** — auth, RBAC, validation, products, cart, wishlist, orders, stock & persistence
- `prisma validate` ✔
- `prisma migrate status` ✔
- `npm run build` ✔
- End-to-end browser flows verified: browse → detail → cart → checkout → order history

---

## 📄 License

MIT — built for the CodeAlpha Full Stack Development Internship.

*Built with production-ready practices and secure authentication.*
