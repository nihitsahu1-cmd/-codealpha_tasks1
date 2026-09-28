# Fieldnote Supply

A small full-stack shop built with HTML, CSS, browser JavaScript, Express, and MongoDB. The same Express server serves the storefront and its JSON API.

## Requirements

- Node.js 18 or newer
- npm
- MongoDB running locally, or a MongoDB Atlas connection string

## Run the project

1. Install dependencies from this folder:

   ```sh
   npm install
   ```

2. Copy `.env.example` to `.env` and set `MONGODB_URI` and `SESSION_SECRET`.

3. Start MongoDB (skip this if using Atlas), then add the example products:

   ```sh
   npm run seed
   ```

4. Start the shop:

   ```sh
   npm start
   ```

5. Open `http://localhost:3000` in your browser.

The seed command is safe to run more than once. It adds the sample products only if they are not already present.

## Configure MongoDB

For a local MongoDB Community Server, use the example connection string:

```env
MONGODB_URI=mongodb://127.0.0.1:27017/simple-shop
```

For MongoDB Atlas, create a free cluster, create a database user, allow your current IP address in Network Access, and copy the Node.js connection string into `MONGODB_URI`. Replace the username, password, and database name in that string. Keep `.env` on your machine and never put its values in frontend files or commit it.

Set `SESSION_SECRET` to a long, random private value. For example, generate one with `node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"` and paste the result into `.env`.

## What's included

- Product browsing, text search, detail pages, and stock-aware cart controls
- Account registration and login with bcrypt password hashing
- MongoDB-backed login sessions
- COD checkout, user-scoped order history, and order status
- Server-side product prices and stock checks when an order is placed

The cart is stored in the browser. Orders, accounts, products, and sessions are stored in MongoDB. Payment is cash on delivery only; no payment gateway is connected.

## API routes

- `POST /api/auth/register`, `POST /api/auth/login`, `POST /api/auth/logout`, `GET /api/auth/me`
- `GET /api/products`, `GET /api/products/:id`
- `POST /api/orders`, `GET /api/orders`, `GET /api/orders/:id` (login required)
- `GET /api/health`

## Project layout

```text
backend/
  config/       MongoDB connection
  controllers/  Request behavior
  middleware/   Login protection
  models/       Mongoose schemas
  routes/        API route definitions
  seed.js        Optional sample catalog
  server.js      Express app and entry point
frontend/
  css/           Responsive storefront styling
  js/            API and page interactions
  *.html         Store, cart, account, and checkout pages
```