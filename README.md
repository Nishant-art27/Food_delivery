# Food Delivery (MERN) — Fullstack Food Ordering App

This repository contains a complete Food Delivery application built with the MERN stack (React + Node/Express + MongoDB). It includes a public frontend for customers, an admin dashboard to manage products and orders, and a backend REST API with authentication and Stripe payment integration.

This README is written so the project is presented as your implementation — replace the placeholder author details with your own information under the "Make it yours" section.

## Table of contents
- About
- Key features
- Tech stack
- Project structure
- Setup (dev)
- Environment variables
- Running (frontend, admin, backend)
- API overview
- Make it yours (ownership steps)
- Troubleshooting & notes

## About

A production-friendly food ordering app with two separate frontends:

- frontend/: Customer-facing React app (browse menu, add to cart, place orders).
- admin/: Admin dashboard (manage products, view orders).
- backend/: Node + Express API with MongoDB, JWT auth, and Stripe payments.

The apps are intentionally small and focused so you can extend them (notifications, analytics, CI/CD, containerization).

## Key features

- Customer-facing features:
    - Browse food items with categories
    - Add to cart, change quantities, remove items
    - User signup/login (JWT)
    - Place orders and view past orders
    - Stripe-based payment flow (server-side charge creation)

- Admin features:
    - Add / edit / delete food items (with image upload)
    - View and manage customer orders
    - Simple role-based access control (admin vs user)

- Backend:
    - RESTful API endpoints for users, foods, carts, and orders
    - Password hashing (bcrypt), JWT authentication
    - File uploads handled with multer (stored in /uploads)

## Tech stack

- Frontend: React (Vite)
- Admin: React (Vite)
- Backend: Node.js, Express
- Database: MongoDB (Atlas or local)
- Auth: JWT
- Payment: Stripe
- File uploads: multer

## Project structure (top-level)

- /frontend — public customer app (React)
- /admin — admin dashboard (React)
- /backend — Express API, controllers, models, routes
- /uploads — uploaded images used by backend

Open these folders to see their own `package.json` and start scripts.

## Setup (local development)

Prerequisites
- Node.js (16+ recommended)
- npm
- MongoDB (Atlas or local)

1) Clone this repository (or use this local copy)

2) Install dependencies for each app. From the repo root run these commands in separate PowerShell tabs:

```powershell
# frontend (customer)
cd frontend; npm install

# admin (dashboard)
cd ..\admin; npm install

# backend (API)
cd ..\backend; npm install
```

3) Create the backend `.env` file. In `backend/` create a `.env` file with at minimum:

```
PORT=5000
MONGO_URL=YOUR_MONGODB_CONNECTION_STRING
JWT_SECRET=some_long_secret_here
SALT=10
STRIPE_SECRET_KEY=sk_test_...
FRONTEND_URL=http://localhost:5173
```

Notes:
- `MONGO_URL` should be your MongoDB Atlas connection string or `mongodb://localhost:27017/food-delivery` for local MongoDB.
- `FRONTEND_URL` should match where you run the customer frontend.

## Running the apps (dev)

Open three PowerShell terminals (or use a multiplexer):

Terminal 1 — Backend
```powershell
cd backend
npm run dev   # or nodemon server.js if configured
```

Terminal 2 — Frontend (customer)
```powershell
cd frontend
npm run dev
```

Terminal 3 — Admin dashboard
```powershell
cd admin
npm run dev
```

After starting, the customer frontend typically runs on http://localhost:5173 and the admin on http://localhost:5174 (check console output or `vite.config.js` port settings).

## API overview

The backend exposes REST endpoints under `/api`. Below are the common routes (adjust paths in your code if different):

- /api/user
    - POST /register — register new user
    - POST /login — login and receive JWT
    - GET /profile — get current user (auth required)

- /api/food
    - GET / — list foods
    - POST / — create food (admin)
    - GET /:id — get single food
    - PUT /:id — update food (admin)
    - DELETE /:id — delete food (admin)

- /api/cart
    - POST / — add item to cart (auth)
    - GET / — get cart items
    - DELETE /:id — remove item

- /api/order
    - POST / — create order (auth)
    - GET / — list orders (admin or user filtered)

Authentication: send `Authorization: Bearer <token>` header for protected routes.

Payments: the backend contains endpoints to create Stripe payment intents/charges — check `orderController.js` for exact routes and payload.

## Uploads

Food images are uploaded to the `backend/uploads` folder and served statically by Express. Make sure this folder exists and your backend serves it (usually via `express.static`).

## Make it yours (remove references & present as your project)

To make this repo clearly yours:

- Update the top-level `README.md` author section below with your name and contact details.
- Remove or change any demo/demo links and replace with your deployed URLs.
- Update `package.json` `author` fields in `frontend`, `admin`, and `backend` if present.
- Set your own Git remote (replacing any existing origin) so the repo points to your GitHub:

```powershell
# replace origin with your new repo
git remote remove origin
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

Note: changing the README and package.json will not rewrite git history — if you need to remove historical references from commits, that's a separate, advanced operation (rewriting history). Use that carefully.

## Troubleshooting

- If a port is already in use, change ports in the `vite.config.js` or the backend `PORT` env.
- If Mongo connection fails, verify `MONGO_URL` and that network access is enabled for Atlas.

## Where to customize next

- Add seed data scripts to populate sample foods.
- Add unit/integration tests.
- Add CI/CD (GitHub Actions) to run lint/tests and deploy.

## Author

Maintained by: Your Name — replace this with your full name, email, and links (LinkedIn/GitHub).

---

If you'd like, I can also:
- update `package.json` author fields to your name,
- add a contributing section with your contact info,
- or help prepare a simple deployment guide for Vercel/Render.

Replace the ownership placeholders and demo links to fully personalize the project.

License: MIT

