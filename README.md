# 🛍️ Forever — Full Stack E-Commerce App

A complete, production-ready e-commerce web application built with the **MERN stack**. Forever consists of three separate apps — a customer-facing storefront, an admin dashboard, and a REST API backend — with full support for user authentication, product management, cart, and payments via **Stripe** and **Razorpay**.

---

## 🏗️ Project Structure

```
forever-full-stack/
├── frontend/      # Customer storefront (React + Vite + Tailwind)
├── admin/         # Admin dashboard (React + Vite + Tailwind)
└── backend/       # REST API server (Node.js + Express + MongoDB)
```

---

## ✨ Features

### 🛒 Customer Frontend
- Browse products with filtering by category, sub-category, and size
- Search bar with live filtering
- Product detail page with image gallery and size selection
- Add to cart, update quantities, remove items
- Checkout with delivery address form
- Payment via **Stripe** or **Razorpay**
- View order history
- User registration and login (JWT-based)
- Responsive design with Tailwind CSS

### 🔧 Admin Dashboard
- Secure admin login (email + password)
- Add new products with image uploads (via Cloudinary)
- List and delete existing products
- View all orders and update order status
- Token-based session persisted in localStorage

### ⚙️ Backend API
- RESTful API with Express.js
- MongoDB database via Mongoose
- JWT authentication for users and admins
- Cloudinary integration for image storage
- Multer for multipart file uploads
- Stripe & Razorpay payment processing
- bcrypt password hashing

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend & Admin | React 18, React Router v6, Tailwind CSS, Vite 5 |
| HTTP Client | Axios |
| Notifications | React Toastify |
| Backend | Node.js, Express.js |
| Database | MongoDB (Mongoose) |
| Auth | JSON Web Tokens (JWT), bcrypt |
| Image Storage | Cloudinary |
| File Uploads | Multer |
| Payments | Stripe, Razorpay |
| Deployment | Vercel (backend `vercel.json` included) |

---

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) v18 or higher
- A [MongoDB Atlas](https://www.mongodb.com/atlas) cluster
- A [Cloudinary](https://cloudinary.com/) account
- A [Stripe](https://stripe.com/) account (for Stripe payments)
- A [Razorpay](https://razorpay.com/) account (for Razorpay payments, optional)

---

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/forever-full-stack.git
cd forever-full-stack
```

---

### 2. Backend Setup

```bash
cd backend
npm install
```

Create a `.env` file in the `backend/` directory:

```env
PORT=4000
JWT_SECRET=your_jwt_secret_key

ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD=your_admin_password

MONGODB_URI=mongodb+srv://<user>:<password>@cluster.mongodb.net/forever

CLOUDINARY_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_SECRET_KEY=your_cloudinary_secret

STRIPE_SECRET_KEY=sk_test_your_stripe_secret_key

RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
```

Start the backend server:

```bash
# Development (with auto-reload)
npm run server

# Production
npm start
```

The API will be running at `http://localhost:4000`.

---

### 3. Frontend Setup

```bash
cd ../frontend
npm install
```

Create a `.env` file in the `frontend/` directory:

```env
VITE_BACKEND_URL=http://localhost:4000
VITE_RAZORPAY_KEY_ID=your_razorpay_key_id
```

Start the frontend:

```bash
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) in your browser.

---

### 4. Admin Dashboard Setup

```bash
cd ../admin
npm install
```

Create a `.env` file in the `admin/` directory:

```env
VITE_BACKEND_URL=http://localhost:4000
```

Start the admin panel:

```bash
npm run dev
```

Open [http://localhost:5174](http://localhost:5174) in your browser and log in with the credentials set in `backend/.env`.

---

## 📡 API Endpoints

### Users — `/api/user`
| Method | Endpoint | Description |
|---|---|---|
| POST | `/register` | Register a new user |
| POST | `/login` | Login and receive a JWT |

### Products — `/api/product`
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| POST | `/add` | Admin | Add a new product with images |
| POST | `/remove` | Admin | Delete a product |
| POST | `/single` | — | Get a single product by ID |
| GET | `/list` | — | Get all products |

### Cart — `/api/cart`
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| POST | `/add` | User | Add item to cart |
| POST | `/update` | User | Update item quantity |
| POST | `/get` | User | Get user's cart |

### Orders — `/api/order`
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| POST | `/place` | User | Place a COD order |
| POST | `/stripe` | User | Place a Stripe order |
| POST | `/razorpay` | User | Place a Razorpay order |
| POST | `/verifyStripe` | User | Verify Stripe payment |
| POST | `/verifyRazorpay` | User | Verify Razorpay payment |
| POST | `/userorders` | User | Get orders for logged-in user |
| POST | `/list` | Admin | Get all orders |
| POST | `/status` | Admin | Update order status |

---

## 🗄️ Data Models

### Product
| Field | Type | Description |
|---|---|---|
| `name` | String | Product name |
| `description` | String | Product description |
| `price` | Number | Price |
| `image` | Array | Cloudinary image URLs |
| `category` | String | e.g. Men, Women, Kids |
| `subCategory` | String | e.g. Topwear, Bottomwear |
| `sizes` | Array | Available sizes (S, M, L, XL, XXL) |
| `bestseller` | Boolean | Featured as bestseller |
| `date` | Number | Timestamp |

### User
Fields include `name`, `email`, `password` (hashed), and `cartData`.

### Order
Fields include `userId`, `items`, `amount`, `address`, `status`, `paymentMethod`, `payment`, and `date`.

---

## 🌐 Deployment

### Backend (Vercel)
A `vercel.json` is already included in the `backend/` folder.

```bash
cd backend
vercel --prod
```

Update `VITE_BACKEND_URL` in both `frontend/.env` and `admin/.env` to point to the deployed backend URL.

### Frontend & Admin (Vercel / Netlify)
```bash
# Frontend
cd frontend && npm run build

# Admin
cd admin && npm run build
```

Deploy the `dist/` folders to Vercel, Netlify, or any static host.

---

## ⚠️ Important Security Notes

> The `.env` files are included in this repository for reference. **Before pushing to GitHub:**

- Rotate all secrets (JWT secret, Cloudinary keys, Stripe keys)
- Add `.env` to your `.gitignore`
- Never commit real API keys or credentials to version control

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
