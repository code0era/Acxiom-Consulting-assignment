# Event Management Command Center (MERN) 🎯

A high-end, production-ready Event Management System built entirely on the MERN stack (MongoDB, Express, React, Node.js). Engineered with a central "Command Center" aesthetic, this multi-portal application allows users to discover services, vendors to manage their offerings, and administrators to oversee the entire platform securely.

## 🚀 Live Demo
**[Insert Vercel Deployment Link Here]**

---

## 🧭 Architecture & Portals

The application uses robust Role-Based Access Control (RBAC) to serve three distinct portals:

### 1. User Portal (Deep Ocean Blue)
*   **Service Discovery**: Users can browse customized event packages (Catering, Decors, Photographers) presented in modern UI cards.
*   **Dynamic Checkout**: A seamless cart system and multi-step payment workflow to confirm event bookings.
*   **Order Tracking**: Real-time visibility into the status of requested services.

### 2. Vendor Hub (Dark Emerald)
*   **Service Registry**: Vendors have dedicated dashboards to add, edit, and price their unique products.
*   **Client Management**: Vendors track incoming orders and can directly view client information (Name/Email) dynamically fetched from the database.
*   **Custom Request Tracking**: Vendors can manage and respond to specialized "Custom Inquiries" from clients.

### 3. Administrator Center (Midnight Indigo)
*   **Subscription & Audit Control**: Admins can approve vendor memberships and oversee service lifecycles.
*   **Identity Management**: Secure oversight of all registered users and vendors in the ecosystem.
*   **System Security Hub**: Allows the overarching administrator to dynamically reset overriding environment passwords securely.

---

## 🎨 Design Philosophy: "The Single-Boundary Box"

The UI breaks away from typical cluttered web components by enforcing a **Single-Border Aesthetic**.
*   All internal container borders were eliminated in favor of a central, high-contrast `.main-boundary-box`.
*   The application looks and feels like an interactive desktop application floating smoothly within the browser.
*   **Fully Responsive**: The main container strategically minimizes to 60% on desktops to retain a premium, tightly grouped layout, while expanding flawlessly to 95% on mobile devices via custom media queries.

---

## ⚙️ Tech Stack

*   **Frontend**: React.js (Vite), Context API (Global Auth State), React Router V6.
*   **Backend**: Node.js, Express.js.
*   **Database**: MongoDB Cloud (Atlas) with Mongoose Object Modeling.
*   **Security**: JSON Web Tokens (JWT) for stateless sessions, Bcrypt.js for database-side password encryption.
*   **Deployment**: Vercel.

---

## 📡 API Documentation & Endpoints

The Express backend strictly enforces JWT-based authentication. Below is the core architecture of the REST API:

### 🔐 Authentication (`/api/auth`)
*   `POST /login` - Authenticates a user/vendor/admin and returns a JWT & role.
*   `POST /signup/user` - Registers a new standard user.
*   `POST /signup/vendor` - Registers a new service vendor (requires admin approval later).

### 🛠️ Administrator Hub (`/api/admin`) *(Requires Admin Token)*
*   `GET /users` - Retrieves a list of all registered clients.
*   `GET /vendors` - Retrieves a list of all vendors and their subscription statuses.
*   `POST /memberships` - Approves or extends a vendor's active membership (1, 6, or 12 months).
*   `DELETE /users/:id` - Revokes access and deletes a user/vendor from the system.
*   `PUT /change-password` - Overrides the global admin gateway password.

### 🏪 Vendor Hub (`/api/vendor`) *(Requires Vendor Token)*
*   `GET /products` - Fetches all services/products owned by the logged-in vendor.
*   `POST /products` - Creates a new service offering (Image, Title, Price, Description).
*   `DELETE /products/:id` - Removes a service offering.
*   `GET /orders` - Fetches all incoming orders placed by clients for this vendor.
*   `PUT /orders/:id` - Updates the fulfillment status of an order (Pending, In Progress, Completed).

### 👥 User Portal (`/api/user`) *(Requires User Token)*
*   `GET /vendors/:category` - Discovers available vendors mapped to a specific category (e.g., Photography).
*   `GET /vendors/:id/products` - Loads a specific vendor's digital storefront of services.
*   `POST /checkout` - Transmits cart sub-items and shipping data to the order database.
*   `GET /orders` - Retrieves the user's historical transactions and real-time status.

---

## 🔧 Local Development Guide

### 1. Prerequisites
Ensure you have Node.js and Git installed. You will also need a MongoDB Atlas URI.

### 2. Configure Environment
Create a `.env` file in the **root** of the `backend` folder:
```env
PORT=5000
MONGODB_URI=your_mongo_connection_string
JWT_SECRET=your_secure_secret_string
```

### 3. Start the Backend
```bash
cd backend
npm install
npm start
```
*The server will spin up on http://localhost:5000*

### 4. Start the Frontend
In a new terminal window:
```bash
cd frontend
npm install
npm run dev
```
*The React UI will run via Vite on http://localhost:5173*

---

## ☁️ Vercel Deployment Structure

This application features a highly optimized monorepo structure for Vercel using `experimentalServices` and `rewrites` to seamlessly fuse the Vite build with Node serverless functions. 

The `vercel.json` and root `package.json` are pre-configured. Simply import the repository to Vercel, leave the root directory as `./`, input your Environment Variables, and click **Deploy**. The custom config will handle the API routing prefix automatically!

---
*Developed as part of the Acxiom Consulting Assignment lifecycle.*
