# 📦 InventoryHub — Modern Product & Inventory Management

> A full-stack React + Express inventory catalog built with **React Router v6**, real REST API communication, client-side form validation, graceful loading & offline error handling, and a responsive mobile-first UI.

---

## 🎯 Requirements & Features Matrix

| Requirement | Implementation Details |
|---|---|
| **✅ At least 3 distinct routes** | 1. **`/`** (Inventory Catalog list with grid & table views, search, filters)<br>2. **`/products/:id`** (Detailed product specifications, SKU, stock status)<br>3. **`/products/new`** & **`/products/:id/edit`** (Validated creation & update forms) |
| **✅ Real API communication** | Communicates with Express REST API (`http://localhost:5000/api/products`) with persistent JSON storage. **Zero hardcoded mock arrays.** |
| **✅ Loading & Error handling** | - Animated spinner while fetching API data.<br>- Graceful error cards with **"Try Again"** button & server diagnosis tips.<br>- Real-time server connectivity health indicator in navbar. |
| **✅ Client-side Form Validation** | Field validation (required lengths, numeric checks, positive prices, valid URLs) before API submission with inline feedback and live card preview. |
| **✅ Clean State Management** | Built using React's native `useState`, `useEffect`, `useMemo`, and a lightweight `ToastContext` for global notification banners. |
| **✅ Fully Responsive Layout** | Clean dark aesthetic, desktop navigation, collapsible mobile menu drawer, responsive metric cards, and adaptive form columns. |

---

## 🚀 Quick Start Guide

### 1. Prerequisites
- **Node.js** (v18.0.0 or higher recommended)
- **npm** (comes with Node.js)

### 2. Installation
Open your terminal in the project directory:
```bash
npm install
```

### 3. Run Backend & Frontend Concurrently (One Command)
```bash
npm run dev
```
This runs both:
- **Backend API Server**: `http://localhost:5000`
- **Vite React Frontend**: `http://localhost:5173`

---

## 🛠 Running Services Individually

If you prefer separate terminal windows:

### Terminal 1: Backend Server
```bash
npm run dev:backend
```
*Runs Express on port 5000 with CORS and JSON database in `server/products.json`.*

### Terminal 2: Frontend App
```bash
npm run dev:frontend
```
*Runs Vite dev server on `http://localhost:5173` with proxy configured for `/api`.*

---

## 🧪 How to Test Key Requirements

### 1. Test Graceful Server Failure & Error Handling
1. Start both servers using `npm run dev`.
2. Open `http://localhost:5173` in your browser. Verify the products load cleanly and the navbar shows **"API Online"** (green dot).
3. Stop the backend server (press `Ctrl + C` in the backend terminal).
4. Click **"Refresh"** on the catalog page or navigate to a product detail view.
5. Notice how the app **does not crash or show a blank screen**:
   - The navbar status pill changes to **"API Offline"** (red dot).
   - An informative Error Card appears with a troubleshooting tip (`npm run dev:backend`) and a **"Try Again"** button.
6. Restart the backend server and click **"Try Again"** — the data smoothly re-loads without needing a browser refresh!

### 2. Test Client-Side Form Validation
1. Click **"Add Product"** (`/products/new`).
2. Try submitting with empty fields:
   - **Product Name**: Must be at least 3 characters.
   - **Category**: Selection required.
   - **Price**: Must be greater than $0.00.
   - **Stock**: Must be a non-negative whole integer.
   - **Description**: Must be at least 10 characters.
   - **Image URL**: Must be a valid `http://` or `https://` link (if provided).
3. Notice the live image and content preview updating on the right as you type.

### 3. Pointing to an External or Custom API
By default, the Vite dev server proxies `/api` requests to `http://localhost:5000`. If you wish to connect to a different API host or port:

Create a `.env` file in the project root:
```env
VITE_API_URL=http://your-custom-api-domain.com/api
```
Restart the frontend server and it will automatically direct all requests to your custom endpoint.

---

## 📡 REST API Reference

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/health` | Health check endpoint returning server status |
| `GET` | `/api/products` | Retrieve all products (supports `?search=` and `?category=`) |
| `GET` | `/api/products/:id` | Get full details for a single product |
| `POST` | `/api/products` | Create a new product (validates schema) |
| `PUT` | `/api/products/:id` | Update an existing product |
| `DELETE` | `/api/products/:id` | Delete a product from inventory |

---

## 📂 Project Structure

```
product-inventory-hub/
├── index.html                   # HTML entry point with Google Fonts
├── vite.config.js               # Vite configuration + API reverse proxy
├── package.json                 # Dependencies and scripts
├── server/
│   ├── server.js                # Express REST API with full CRUD endpoints
│   └── products.json            # Persistent JSON database with seed data
├── src/
│   ├── main.jsx                 # React root + BrowserRouter
│   ├── App.jsx                  # Main router setup & layout
│   ├── index.css                # Polished responsive design system
│   ├── services/
│   │   └── api.js               # Fetch API client with timeout & error parser
│   ├── context/
│   │   └── ToastContext.jsx     # Global toast notification provider
│   ├── components/
│   │   ├── Navbar.jsx           # Responsive header + API health indicator
│   │   ├── ProductCard.jsx      # Inventory card with stock badges
│   │   ├── LoadingSpinner.jsx   # Visual spinner state
│   │   ├── ErrorMessage.jsx     # Error alert card with retry action
│   │   └── ConfirmModal.jsx     # Safe deletion confirmation modal
│   └── pages/
│       ├── ProductListPage.jsx  # Route: / (Catalog list, filters, metrics)
│       ├── ProductDetailPage.jsx# Route: /products/:id (Detailed view)
│       ├── ProductFormPage.jsx  # Route: /products/new & /products/:id/edit
│       └── NotFoundPage.jsx     # Route: * (404 Fallback page)
└── README.md
```

---

## 💻 Tech Stack
- **Frontend**: React 18, React Router v6, Lucide React Icons, Vite
- **Backend**: Node.js, Express, CORS
- **Styling**: Modern Vanilla CSS Design System with CSS variables and responsive media queries
