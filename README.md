**Budgenix** – A modern, full‑stack personal budgeting web application  
============================================================


![Budgenix Logo](https://raw.githubusercontent.com/kaihere14/Budgenix/main/client/public/vite.svg)

[![Node.js](https://img.shields.io/badge/Node.js-20.x-brightgreen?logo=node.js)](https://nodejs.org/)  
[![React](https://img.shields.io/badge/React-18.2.0-blue?logo=react)](https://reactjs.org/)  
[![Vite](https://img.shields.io/badge/Vite-5.0.0-yellow?logo=vite)](https://vitejs.dev/)  
[![TypeScript](https://img.shields.io/badge/TypeScript-5.3.3-blue?logo=typescript)](https://www.typescriptlang.org/)  
[![Express](https://img.shields.io/badge/Express-4.19.2-lightgrey?logo=express)](https://expressjs.com/)  
[![MongoDB](https://img.shields.io/badge/MongoDB-7.0.0-green?logo=mongodb)](https://www.mongodb.com/)  
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)  
[![Version](https://img.shields.io/badge/version-1.0.1-blue?logo=semantic-release)](https://github.com/kaihere14/Budgenix/releases/tag/v1.0.1)  
[![GitHub last commit](https://img.shields.io/github/last-commit/kaihere14/Budgenix)](https://github.com/kaihere14/Budgenix/commits/main)

---

## Overview

Budgenix is a **single‑page web app** that helps users track income, expenses, savings goals, and recurring transactions in real time. Built with a **React + Vite** front‑end and a **Node/Express + TypeScript** back‑end, it stores data in **MongoDB** and provides a clean, responsive UI for budgeting on desktop and mobile.

- **Why Budgenix?**  
  - No ads, no hidden fees – completely open source.  
  - Real‑time charts powered by Chart.js.  
  - Secure JWT authentication and role‑based access.  

Target audience: individuals, freelancers, and small teams who need a lightweight, self‑hosted budgeting tool.

Current stable version: **v1.0.1** (released 2024‑12‑01).

---

## Features

| Feature | Description | Status |
|---------|-------------|--------|
| **User Authentication** | Register / login with email & password, JWT‑based sessions. | ✅ Stable |
| **Dashboard** | Overview of total income, expenses, net balance, and recent activity. | ✅ Stable |
| **Expense / Income CRUD** | Create, read, update, delete transactions with categories & tags. | ✅ Stable |
| **Budget Categories** | Custom categories (Food, Transport, etc.) with optional limits. | ✅ Stable |
| **Savings Goals** | Set target amounts and track progress over time. | ✅ Stable |
| **Recurring Transactions** | Define transactions that repeat on a schedule (daily, weekly, monthly). | ✅ Stable |
| **Responsive UI** | Mobile‑first layout, works on all modern browsers. | ✅ Stable |
| **Data Export** | Export transactions as CSV for external analysis. | 🟡 Beta |
| **Multi‑currency Support** | Store amounts in different currencies (future work). | 🟠 Experimental |
| **Dark Mode** | Toggle between light and dark themes. | ✅ Stable |

---

## Tech Stack

| Layer | Technology | Reason |
|-------|------------|--------|
| **Front‑end** | React 18, Vite, JSX, TailwindCSS (optional) | Fast HMR, modern React features |
| **State Management** | React Context + custom hooks | Simple, no extra boilerplate |
| **Charts** | Chart.js (via `react-chartjs-2`) | Interactive visualisations |
| **Back‑end** | Node.js 20, Express, TypeScript | Type safety, scalable routing |
| **Database** | MongoDB (via Mongoose) | Flexible document model for transactions |
| **Authentication** | JSON Web Tokens (JWT) + bcrypt | Secure password storage |
| **Testing** | Jest + React Testing Library (client) <br> Jest + Supertest (server) | Unit & integration coverage |
| **Containerisation** | Docker (multi‑stage) | One‑click dev/prod environments |
| **CI/CD** | GitHub Actions (build, lint, test) | Automated quality gates |

---

## Architecture

```
root
├─ client/                # React front‑end (Vite)
│   ├─ src/
│   │   ├─ components/    # UI components (Header, Card, Chart, etc.)
│   │   ├─ pages/         # Route‑level pages (Dashboard, Login, Settings)
│   │   ├─ context/       # Global state (AuthContext, BudgetContext)
│   │   ├─ hooks/         # Reusable custom hooks (useFetch, useForm)
│   │   └─ assets/        # Images, icons
│   └─ vite.config.js
└─ server/                # Express API (TypeScript)
    ├─ src/
    │   ├─ controllers/   # Request handlers (auth.controller.ts, transaction.controller.ts)
    │   ├─ models/        # Mongoose schemas (User, Transaction, Category, Goal, Recurrence)
    │   ├─ routes/        # Express routers (auth.routes.ts, transaction.routes.ts)
    │   ├─ middleware/    # Auth, error handling, validation
    │   ├─ databases/     # MongoDB connection logic
    │   └─ types/         # Shared TypeScript interfaces
    └─ index.ts           # Server entry point
```

*Data Flow*:  

1. **Client** sends HTTP requests (Axios) to `/api/*` endpoints.  
2. **Server** validates JWT, processes request via controller, interacts with MongoDB, returns JSON.  
3. **Client** updates React state, re‑renders UI.

---

## Getting Started

### Prerequisites

| Tool | Minimum version |
|------|-----------------|
| Node.js | 20.x |
| npm or pnpm | 9.x |
| Docker (optional) | 24.x |
| MongoDB | 7.x (local or Atlas) |
| Git | 2.40+ |

### Installation (Local Development)

1. **Clone the repository**

   ```bash
   git clone https://github.com/kaihere14/Budgenix.git
   cd Budgenix
   ```

2. **Set up environment variables**

   Create a `.env` file in the **server** folder:

   ```dotenv
   # server/.env
   PORT=5000
   MONGO_URI=mongodb://localhost:27017/budgenix
   JWT_SECRET=yourSuperSecretKey
   JWT_EXPIRES_IN=7d
   ```

   Create a `.env` file in the **client** folder (optional, only needed for custom API URLs):

   ```dotenv
   # client/.env
   VITE_API_URL=http://localhost:5000/api
   ```

3. **Install dependencies**

   ```bash
   # Server dependencies
   cd server
   pnpm install   # or npm install

   # Client dependencies
   cd ../client
   pnpm install   # or npm install
   ```

4. **Run the development servers**

   ```bash
   # In one terminal – back‑end
   cd server
   pnpm dev   # runs ts-node-dev (npm script defined in server/package.json)

   # In another terminal – front‑end
   cd client
   pnpm dev   # runs Vite dev server
   ```

   The client will be available at `http://localhost:5173` and proxies API calls to `http://localhost:5000`.

5. **Verify the setup**

   - Open the browser → `http://localhost:5173`.
   - Register a new account, log in, and you should see the dashboard.

### Docker (Production‑ready)

A multi‑stage Dockerfile is provided for both client and server.

```bash
# Build and run everything with Docker Compose (if you add a compose file)
docker compose up --build
```

The app will be reachable at `http://localhost:80`.

---

## Usage

### Authentication

```bash
# Register
POST /api/auth/register
{
  "email": "john@example.com",
  "password": "StrongP@ssw0rd"
}

# Login
POST /api/auth/login
{
  "email": "john@example.com",
  "password": "StrongP@ssw0rd"
}
# Response contains JWT token
```

All subsequent requests must include the token:

```
Authorization: Bearer <jwt-token>
```

### Transaction CRUD (example with Axios)

```javascript
import axios from 'axios';

const api = axios.create({
  baseURL: import.meta.env.VITE_API_URL,
  headers: {
    Authorization: `Bearer ${localStorage.getItem('token')}`
  }
});

// Create a new expense
await api.post('/transactions', {
  type: 'expense',
  amount: 45.99,
  category: 'Food',
  date: '2024-12-01',
  note: 'Dinner at sushi place'
});

// Get all transactions
const { data } = await api.get('/transactions');
console.log(data);
```

### Recurring Transactions

```bash
# Create a recurring transaction (monthly)
POST /api/recurrences
{
  "type": "expense",
  "amount": 120,
  "category": "Gym",
  "frequency": "monthly",
  "startDate": "2024-12-01",
  "note": "Gym membership"
}
```

The server will automatically generate a concrete transaction each period.

### Dashboard

The dashboard page (`/dashboard`) displays:

- **Net Balance** (income – expenses)
- **Monthly Spend Chart** (Chart.js line chart)
- **Recent Transactions** (table with edit/delete actions)
- **Savings Goal Progress** (circular progress bar)
- **Upcoming Recurrences** (list of scheduled transactions)

### Export CSV

```bash
GET /api/transactions/export
# Returns a CSV file with all user transactions
```

---

## API Documentation

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| `POST` | `/api/auth/register` | Create a new user account | ❌ |
| `POST` | `/api/auth/login` | Authenticate and receive JWT | ❌ |
| `GET`  | `/api/users/me` | Get current user profile | ✅ |
| `GET`  | `/api/transactions` | List all user transactions (filterable) | ✅ |
| `POST` | `/api/transactions` | Add a new transaction | ✅ |
| `PUT`  | `/api/transactions/:id` | Update a transaction | ✅ |
| `DELETE`| `/api/transactions/:id` | Delete a transaction | ✅ |
| `GET`  | `/api/categories` | Retrieve all budget categories | ✅ |
| `POST` | `/api/categories` | Create a new category | ✅ |
| `GET`  | `/api/goals` | List savings goals | ✅ |
| `POST` | `/api/goals` | Create a new goal | ✅ |
| `GET`  | `/api/recurrences` | List recurring transactions | ✅ |
| `POST` | `/api/recurrences` | Create a new recurrence | ✅ |
| `GET`  | `/api/transactions/export` | Export transactions as CSV | ✅ |

### Request / Response Example – Create Transaction

**Request**

```json
POST /api/transactions
{
  "type": "income",
  "amount": 1200,
  "category": "Salary",
  "date": "2024-12-01",
  "note": "December salary"
}
```

**Response**

```json
{
  "success": true,
  "transaction": {
    "_id": "66a1f2c4e5b9c9d4f7a1b2c3",
    "type": "income",
    "amount": 1200,
    "category": "Salary",
    "date": "2024-12-01T00:00:00.000Z",
    "note": "December salary",
    "user": "66a1e9b1e5b9c9d4f7a1a9b8",
    "createdAt": "2024-07-30T12:34:56.789Z",
    "updatedAt": "2024-07-30T12:34:56.789Z"
  }
}
```

### Error Handling

All error responses follow the same shape:

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Amount must be a positive number."
  }
}
```

Common error codes:

- `AUTHENTICATION_ERROR` – missing/invalid JWT.  
- `VALIDATION_ERROR` – request body fails schema validation.  
- `NOT_FOUND` – resource does not exist.  
- `SERVER_ERROR` – unexpected server failure.

---

## Development

### Running Tests

```bash
# Server tests
cd server
pnpm test   # runs jest with ts-jest

# Client tests
cd ../client
pnpm test   # runs jest + @testing-library/react
```

### Linting & Formatting

```bash
# Server
pnpm lint   # ESLint (typescript-eslint)

# Client
pnpm lint   # ESLint (React)
pnpm format # Prettier
```

### Debugging

- **Server**: `pnpm dev` runs `ts-node-dev` with source‑maps. Use VS Code launch config `"type": "node"` and attach to port `9229`.  
- **Client**: Vite dev server provides hot‑module replacement. Open Chrome DevTools → React DevTools for component inspection.

### Contributing a New Feature

1. Fork the repo and create a feature branch (`git checkout -b feat/your-feature`).  
2. Follow the existing folder conventions (`client/src/...`, `server/src/...`).  
3. Add unit/integration tests.  
4. Run `pnpm lint && pnpm test` locally.  
5. Submit a PR with a clear description and screenshots (if UI changes).

---

## Deployment

### Production Build (Docker)

```dockerfile
# server/Dockerfile
FROM node:20-alpine AS builder
WORKDIR /app
COPY server/package*.json ./
RUN npm ci
COPY server/ .
RUN npm run build   # compiles TypeScript

FROM node:20-alpine AS runtime
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY server/package*.json ./
RUN npm ci --production
EXPOSE 5000
CMD ["node", "dist/index.js"]
```

```dockerfile
# client/Dockerfile
FROM node:20-alpine AS builder
WORKDIR /app
COPY client/package*.json ./
RUN npm ci
COPY client/ .
RUN npm run build   # Vite production build

FROM nginx:stable-alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
```

Deploy the two containers behind a reverse proxy (NGINX, Traefik, or your cloud provider). Ensure the `VITE_API_URL` environment variable points to the back‑end URL.

### Vercel (Front‑end)

The `client/vercel.json` is already configured for static deployment. Connect the repository to Vercel, set the environment variable `VITE_API_URL`, and Vercel will handle builds automatically.

### Heroku / Render (Back‑end)

```bash
heroku create budgenix-api
git push heroku main:master
heroku config:set MONGO_URI=<your-mongo-uri> JWT_SECRET=<secret>
```

---

## Contributing

We welcome contributions! Please read our **[CONTRIBUTING.md](CONTRIBUTING.md)** for details on our code of conduct, the pull‑request process, and how to report bugs.

1. **Fork** the repository.  
2. **Create a branch** (`git checkout -b feat/awesome-feature`).  
3. **Commit** your changes with clear messages.  
4. **Push** to your fork (`git push origin feat/awesome-feature`).  
5. **Open a Pull Request** against