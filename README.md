# StyleAura

<p align="center">
  <img src="client/public/sa_logo.png" alt="StyleAura logo" width="120" />
</p>

<h3 align="center">Fashion, beauty, affiliate shopping, and editorial content in one full-stack experience.</h3>

<p align="center">
  <a href="#features">Features</a> |
  <a href="#tech-stack">Tech Stack</a> |
  <a href="#quick-start">Quick Start</a> |
  <a href="#environment-variables">Environment</a> |
  <a href="#api-overview">API</a> |
  <a href="#deployment">Deployment</a>
</p>

<p align="center">
  <img alt="React" src="https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=111" />
  <img alt="Vite" src="https://img.shields.io/badge/Vite-5-646CFF?style=for-the-badge&logo=vite&logoColor=fff" />
  <img alt="Tailwind CSS" src="https://img.shields.io/badge/Tailwind_CSS-3-38BDF8?style=for-the-badge&logo=tailwindcss&logoColor=fff" />
  <img alt="Node.js" src="https://img.shields.io/badge/Node.js-Express-339933?style=for-the-badge&logo=nodedotjs&logoColor=fff" />
  <img alt="MongoDB" src="https://img.shields.io/badge/MongoDB-Mongoose-47A248?style=for-the-badge&logo=mongodb&logoColor=fff" />
</p>

---

## Preview

<p align="center">
  <img src="client/public/home.png" alt="StyleAura home preview" width="31%" />
  <img src="client/public/shop.png" alt="StyleAura shop preview" width="31%" />
  <img src="client/public/outfit.png" alt="StyleAura outfit preview" width="31%" />
</p>

StyleAura is a full-stack lifestyle platform for publishing fashion and beauty blogs, curating affiliate products, tracking engagement, collecting newsletter subscribers, and managing everything from a protected admin dashboard.

---

## Features

| Experience | What it includes |
| --- | --- |
| Editorial blog | Fashion and beauty articles, rich text content, categories, tags, likes, comments, related posts, and SEO fields. |
| Affiliate shop | Product pages, image galleries, ratings, pros and cons, affiliate click tracking, trending products, and category browsing. |
| User tools | Login/signup, bookmarks, liked posts, search, cookie consent, and dark mode support. |
| Admin dashboard | Protected admin routes for managing blogs, products, analytics, and content uploads. |
| Growth layer | Newsletter subscriptions, Pinterest-friendly metadata, sitemap/static policy pages, and affiliate disclosure pages. |
| Media handling | Cloudinary-backed image upload pipeline with Multer validation. |

<details>
<summary><strong>Click to explore the route map</strong></summary>

### Public Routes

| Route | Page |
| --- | --- |
| `/` | Home |
| `/blog/:slug` | Blog details |
| `/product/:slug` | Product details |
| `/shop` | Affiliate shop |
| `/outfits` | Outfit inspiration |
| `/search` | Search results |
| `/bookmarks` | Saved content |
| `/login` | User auth |
| `/about`, `/contact`, `/privacy-policy`, `/disclaimer`, `/affiliate-disclosure`, `/terms-and-conditions`, `/sitemap` | Static pages |

### Admin Routes

| Route | Page |
| --- | --- |
| `/admin/login` | Admin login |
| `/admin` | Dashboard |
| `/admin/blogs` | Manage blogs |
| `/admin/products` | Manage products |
| `/admin/analytics` | Analytics |

</details>

---

## Tech Stack

### Frontend

- React 18 with Vite
- Tailwind CSS
- React Router
- TanStack React Query
- Axios
- Framer Motion
- React Hot Toast
- React Quill
- Recharts
- React Helmet Async

### Backend

- Node.js
- Express
- MongoDB with Mongoose
- JWT authentication
- Cookie-based auth support
- Cloudinary uploads
- Multer file handling
- Morgan request logging
- Nodemailer-ready dependency layer

---

## Project Structure

```txt
StyleAura/
  client/
    public/              # Brand and page imagery
    src/
      components/        # Common, blog, product, and admin UI
      context/           # Auth, bookmarks, and theme state
      hooks/             # Debounce and infinite scroll helpers
      pages/             # Public and admin routes
      services/api.js    # Axios API client
  server/
    config/              # Database connection
    controllers/         # Request handlers
    middleware/          # Auth and upload middleware
    models/              # Mongoose schemas
    routes/              # Express route modules
    utils/               # Cloudinary helpers
  render.yaml            # Render deployment blueprint
```

---

## Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/your-username/StyleAura.git
cd StyleAura
```

### 2. Install dependencies

```bash
cd server
npm install

cd ../client
npm install
```

### 3. Configure environment variables

Create `.env` files for the server and client using the examples below.

### 4. Run the backend

```bash
cd server
npm run dev
```

The API starts at:

```txt
http://localhost:5000
```

### 5. Run the frontend

```bash
cd client
npm run dev
```

The app starts at:

```txt
http://localhost:5173
```

---

## Environment Variables

### `server/.env`

```env
NODE_ENV=development
PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
JWT_EXPIRE=7d
ADMIN_SECRET=your_one_time_admin_registration_secret
ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD=replace_with_a_strong_password
CLIENT_URL=http://localhost:5173

CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

You can also configure Cloudinary with `CLOUDINARY_URL` if preferred.

### `client/.env`

```env
VITE_API_URL=http://localhost:5000/api
VITE_API_BASE_URL=http://localhost:5000
```

---

## Admin Setup

Create the first admin account in either of these ways:

### Option A: Seed from environment variables

```bash
cd server
node seedAdmin.js
```

This uses `ADMIN_EMAIL` and `ADMIN_PASSWORD` from `server/.env`.

### Option B: Register with the admin secret

Send a request to:

```txt
POST /api/auth/register
```

With:

```json
{
  "email": "admin@example.com",
  "password": "replace_with_a_strong_password",
  "secret": "your_one_time_admin_registration_secret"
}
```

---

## API Overview

<details open>
<summary><strong>Authentication</strong></summary>

| Method | Endpoint | Description |
| --- | --- | --- |
| `POST` | `/api/auth/login` | Login admin/user |
| `POST` | `/api/auth/signup` | Register public user |
| `GET` | `/api/auth/me` | Get current authenticated user |
| `POST` | `/api/auth/logout` | Logout |
| `POST` | `/api/auth/register` | Register an admin with `ADMIN_SECRET` |

</details>

<details>
<summary><strong>Blogs</strong></summary>

| Method | Endpoint | Description |
| --- | --- | --- |
| `GET` | `/api/blogs` | List published blogs |
| `GET` | `/api/blogs/:slug` | Get blog details |
| `POST` | `/api/blogs` | Create blog |
| `PUT` | `/api/blogs/:id` | Update blog |
| `DELETE` | `/api/blogs/:id` | Delete blog |
| `POST` | `/api/blogs/:id/like` | Like blog |
| `POST` | `/api/blogs/:id/comments` | Add comment |
| `GET` | `/api/blogs/admin/all` | Admin blog list |

</details>

<details>
<summary><strong>Products</strong></summary>

| Method | Endpoint | Description |
| --- | --- | --- |
| `GET` | `/api/products` | List products |
| `GET` | `/api/products/:slug` | Get product details |
| `POST` | `/api/products` | Create product |
| `PUT` | `/api/products/:id` | Update product |
| `DELETE` | `/api/products/:id` | Delete product |
| `POST` | `/api/products/:id/click` | Track affiliate click |
| `GET` | `/api/products/admin/all` | Admin product list |

</details>

<details>
<summary><strong>Users, Analytics, Newsletter</strong></summary>

| Method | Endpoint | Description |
| --- | --- | --- |
| `GET` | `/api/users/bookmarks` | Get user bookmarks |
| `POST` | `/api/users/bookmarks` | Add bookmark |
| `DELETE` | `/api/users/bookmarks/:itemId` | Remove bookmark |
| `GET` | `/api/users/likes` | Get liked blogs |
| `GET` | `/api/analytics/summary` | Get admin analytics summary |
| `POST` | `/api/newsletter/subscribe` | Subscribe to newsletter |
| `GET` | `/api/health` | Health check |

</details>

---

## Deployment

The repository includes a `render.yaml` blueprint with:

- A Node web service for the Express API from `server/`
- A static site for the Vite client from `client/`
- SPA fallback routing to `index.html`

For production, set these values in your hosting provider:

- `MONGO_URI`
- `JWT_SECRET`
- `ADMIN_SECRET`
- `CLIENT_URL`
- Cloudinary credentials
- `VITE_API_URL`
- `VITE_API_BASE_URL`

Make sure the backend CORS allowlist includes your deployed frontend URL.

---

## Useful Scripts

| Location | Command | Description |
| --- | --- | --- |
| `client` | `npm run dev` | Start Vite dev server |
| `client` | `npm run build` | Build frontend for production |
| `client` | `npm run preview` | Preview production build |
| `server` | `npm run dev` | Start API with Nodemon |
| `server` | `npm start` | Start API with Node |
| `server` | `node seedAdmin.js` | Create first admin account |

---

## Security Notes

- Keep `.env` files out of version control.
- Use a strong `JWT_SECRET` in production.
- Rotate `ADMIN_SECRET` after creating the first admin account.
- Use HTTPS in production so auth cookies are sent securely.
- Verify Cloudinary upload rules and file size limits before public launch.

---

## Roadmap Ideas

- Add automated tests for API controllers and protected routes.
- Add role-based permissions beyond admin/user.
- Add email delivery for newsletter workflows.
- Add product collections and outfit boards.
- Add dashboard charts for traffic, clicks, likes, and conversions.

---

</p>
