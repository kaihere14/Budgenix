# Budgenix  
**A modern, full‑stack budgeting platform**  



---

## Badges  

| Build | Coverage | Version | License |
|-------|----------|---------|---------|
| ![CI](https://github.com/kaihere14/Budgenix/actions/workflows/ci.yml/badge.svg) | ![Coverage](https://codecov.io/gh/kaihere14/Budgenix/branch/main/graph/badge.svg) | ![npm](https://img.shields.io/npm/v/budgenix.svg) | ![License](https://img.shields.io/github/license/kaihere14/Budgenix) |

**Quick links**: [Demo](#demo) • [Documentation](#documentation) • [Issues](https://github.com/kaihere14/Budgenix/issues) • [Pull Requests](https://github.com/kaihere14/Budgenix/pulls)

---

## Overview  

Budgenix is an open‑source personal finance manager that helps users track income, expenses, and budgets in real time. Built with a **React + Vite** front‑end and a **Node.js/Express + TypeScript** back‑end, it offers a clean UI, RESTful API, and optional Docker deployment.

* **Why Budgenix?**  
  * Zero‑cost, self‑hosted alternative to SaaS budgeting tools.  
  * Real‑time charts and insights powered by Chart.js.  
  * Extensible architecture – add new data sources or analytics with minimal friction.

*Target audience*: developers who want a ready‑made budgeting starter‑kit, hobbyists looking for a self‑hosted finance tracker, and anyone interested in learning a modern full‑stack TypeScript stack.

Current version: **v1.3.0** (2025‑12‑15)

---

## Features  

| Feature | Description | Status |
|---------|-------------|--------|
| **User authentication** | JWT‑based sign‑up / login with password hashing (bcrypt). | Stable |
| **Multi‑currency support** | Store amounts in any ISO‑4217 currency; automatic conversion via ExchangeRate‑API. | Stable |
| **Budget creation & tracking** | Define monthly budgets per category; visual progress bars. | Stable |
| **Transaction management** | CRUD for income & expense entries, bulk import (CSV). | Stable |
| **Recurring transactions** | Define repeatable income/expense entries (daily, weekly, monthly). | New / Stable |
| **Dynamic dashboards** | Interactive charts (spending over time, category breakdown). | Stable |
| **Responsive UI** | Mobile‑first design, works on all modern browsers. | Stable |
| **RESTful API** | Full OpenAPI‑compatible spec, ready for third‑party integrations. | Stable |
| **Docker support** | One‑command containerised deployment. | Beta |
| **Webhooks** | Optional webhook notifications for budget overruns. | Experimental |

---

## Tech Stack  

| Layer | Technology | Reason |
|-------|------------|--------|
| **Front‑end** | React 18, Vite, TailwindCSS, Chart.js, Axios | Fast HMR, utility‑first styling, lightweight bundle |
| **Back‑end** | Node.js 20, Express, TypeScript, Prisma ORM | Type‑safe server, easy DB migrations |
| **Database** | PostgreSQL 15 (default) | Relational, ACID‑compliant, scalable |
| **Auth** | JWT, bcrypt | Stateless, widely supported |
| **Containerisation** | Docker, Docker‑Compose | Reproducible environments |
| **Testing** | Vitest (client), Jest + Supertest (server) | Unit & integration coverage |
| **CI/CD** | GitHub Actions | Automated lint, test, build pipelines |
| **Other** | dotenv, cors, helmet, morgan | Environment handling & security |

---

## Architecture  

```
root
├─ client/                # React + Vite SPA
│   ├─ src/
│   │   ├─ components/    # UI components (Chart, Form, Card, …)
│   │   ├─ pages/         # Route‑level pages (Dashboard, Budgets, Settings)
│   │   ├─ context/       # React Context providers (Auth, Budget)
│   │   ├─ hooks/         # Custom hooks (useFetch, useAuth)
│   │   └─ assets/
│   └─ vite.config.js
│
├─ server/                # Express API (TypeScript)
│   ├─ src/
│   │   ├─ controllers/   # Request handlers (auth.controller.ts, budget.controller.ts, transaction.controller.ts)
│   │   ├─ routes/        # Express routers (auth.routes.ts, budget.routes.ts, transaction.routes.ts, recurring.routes.ts)
│   │   ├─ models/        # Prisma schema + TypeScript types
│   │   ├─ middleware/    # Auth guard, error handler, request logger, rate limiter
│   │   ├─ databases/     # Prisma client init
│   │   └─ types/         # Shared TypeScript interfaces
│   └─ index.ts           # Server bootstrap
│
├─ docker-compose.yml     # Multi‑service orchestration
└─ .env.example           # Environment variable template
```

* **Client ↔ Server** – communication via Axios; base URL taken from `VITE_API_URL` environment variable.  
* **Server** – all routes are versioned under `/api/v1`.  
* **Database** – Prisma migrations live in `server/prisma/migrations`.  

---

## Getting Started  

### Prerequisites  

| Tool | Minimum version |
|------|-----------------|
| Node.js | 20.x |
| pnpm (recommended) | 8.x |
| Docker & Docker‑Compose (optional) | 24.x |
| PostgreSQL (if not using Docker) | 15.x |
| Git | any |

> **Note**: The project uses **pnpm** for deterministic lockfiles, but `npm` or `yarn` work as well.

### Installation  

#### 1. Clone the repository  

```bash
git clone https://github.com/kaihere14/Budgenix.git
cd Budgenix
```

#### 2. Set up environment variables  

```bash
# copy the template and edit as needed
cp .env.example .env
# open .env in your editor and fill in the values
```

**Server side (`.env`)**

```dotenv
PORT=4000
DATABASE_URL=postgresql://budgenix_user:password@localhost:5432/budgenix_db
JWT_SECRET=super_secret_key
EXCHANGE_API_KEY=your_exchangerate_api_key
```

**Client side (`.env` – Vite loads variables prefixed with `VITE_`)**

```dotenv
VITE_API_URL=http://localhost:4000/api/v1
```

#### 3. Install dependencies  

```bash
# Server
cd server
pnpm install

# Client
cd ../client
pnpm install
```

#### 4. Run the database (Docker‑compose) – *optional*  

```bash
docker compose up -d postgres
# wait a few seconds for PostgreSQL to become ready
```

#### 5. Apply Prisma migrations  

```bash
cd ../server
pnpm prisma migrate deploy   # creates tables if they don't exist
```

#### 6. Start the applications  

```bash
# In one terminal – API server
cd server
pnpm dev                    # runs `ts-node-dev src/index.ts`

# In another terminal – Front‑end
cd ../client
pnpm dev                    # runs `vite`
```

The client will be available at **http://localhost:5173** and the API at **http://localhost:4000/api/v1**.

### Verification  

Open the browser at the client URL. You should see the Budgenix landing page and be able to register a new user.

---

## Usage  

### Register & Login (via UI)  

1. Click **Sign Up**, fill in email & password.  
2. After registration, you are automatically logged in and redirected to the Dashboard.

### Dashboard  

- **Spending Overview** – line chart of expenses over the last 30 days.  
- **Budget Progress** – circular progress bars per category.  

### API Quick Reference  

All endpoints are prefixed with `/api/v1`. Authentication is required for every route except `/auth/*`. Include the JWT token in the `Authorization` header:

```http
Authorization: Bearer <your_jwt_token>
```

#### Auth  

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/auth/register` | Register a new user. Body: `{ email, password }` |
| `POST` | `/auth/login`    | Login and receive JWT. Body: `{ email, password }` |
| `GET`  | `/auth/me`       | Get current user profile (requires JWT). |

**Example – Register**

```bash
curl -X POST http://localhost:4000/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{"email":"alice@example.com","password":"StrongP@ssw0rd"}'
```

#### Budgets  

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET`  | `/budgets` | List all budgets for the authenticated user. |
| `POST` | `/budgets` | Create a new budget. Body: `{ name, limit, currency, month }` |
| `GET`  | `/budgets/:id` | Retrieve a single budget. |
| `PUT`  | `/budgets/:id` | Update budget fields. |
| `DELETE`| `/budgets/:id`| Delete a budget. |

**Example – Create a Budget**

```bash
curl -X POST http://localhost:4000/api/v1/budgets \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
        "name": "Groceries",
        "limit": 300,
        "currency": "USD",
        "month": "2025-01"
      }'
```

#### Transactions  

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET`  | `/transactions` | List transactions (filterable by date, category). |
| `POST` | `/transactions` | Add a new transaction. Body: `{ amount, currency, date, category, description }` |
| `PUT`  | `/transactions/:id` | Update a transaction. |
| `DELETE`| `/transactions/:id`| Delete a transaction. |

**Example – Add a Transaction**

```bash
curl -X POST http://localhost:4000/api/v1/transactions \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
        "amount": 45.99,
        "currency": "USD",
        "date": "2025-01-15",
        "category": "Groceries",
        "description": "Weekly supermarket"
      }'
```

#### Recurring Transactions  

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET`  | `/recurring` | List all recurring entries for the user. |
| `POST` | `/recurring` | Create a recurring transaction. Body: `{ amount, currency, startDate, frequency, category, description }` |
| `PUT`  | `/recurring/:id` | Update a recurring entry. |
| `DELETE`| `/recurring/:id`| Remove a recurring entry. |

**Example – Create a Monthly Subscription**

```bash
curl -X POST http://localhost:4000/api/v1/recurring \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
        "amount": 9.99,
        "currency": "USD",
        "startDate": "2025-01-01",
        "frequency": "monthly",
        "category": "Entertainment",
        "description": "Streaming service"
      }'
```

Full OpenAPI spec is available at `http://localhost:4000/api/v1/docs` when the server is running.

---

## Development  

### Setting up a local dev environment  

```bash
# Server
cd server
pnpm install
pnpm prisma generate   # generate Prisma client types
pnpm dev               # starts ts-node-dev with hot reload

# Client
cd ../client
pnpm install
pnpm dev               # Vite dev server with HMR
```

### Running tests  

```bash
# Server tests (Jest + Supertest)
cd server
pnpm test

# Client tests (Vitest)
cd ../client
pnpm test
```

### Code style  

- **ESLint** (client) – configured with `eslint.config.js`.  
- **Prettier** – enforced via `pnpm format`.  
- **TypeScript** – strict mode (`"strict": true` in `tsconfig.json`).  

### Debugging  

- Server: use `pnpm dev:debug` to launch with `--inspect`.  
- Client: open Chrome DevTools; Vite provides source‑map support out of the box.

---

## Deployment  

### Docker (recommended)  

```bash
# Build and start all services (PostgreSQL, API, client)
docker compose up --build -d
```

The client will be served by Nginx on port **80**, the API on **4000** (internal).  

### Production (manual)  

1. **Build client**  

   ```bash
   cd client
   pnpm build   # outputs to ./dist
   ```

2. **Run server**  

   ```bash
   cd ../server
   pnpm install --prod
   NODE_ENV=production pnpm start   # uses compiled JS from ./dist
   ```

3. **Serve static files** – configure your favourite reverse proxy (NGINX, Caddy) to serve `client/dist` and proxy `/api` to the Node server.

### Environment variables for production  

| Variable | Description |
|----------|-------------|
| `PORT` | Port on which the API listens (default 4000). |
| `DATABASE_URL` | PostgreSQL connection string. |
| `JWT_SECRET` | Strong secret for signing JWTs. |
| `EXCHANGE_API_KEY` | API key for currency conversion service. |
| `VITE_API_URL` | Base URL for the client to reach the API (e.g., `https://api.budgenix.com/api/v1`). |

---

## API Documentation  

The API follows **OpenAPI 3.1**. After starting the server, visit:

```
http://localhost:4000/api/v1/docs
```

You’ll find an interactive Swagger UI with:

* **Authentication** – Bearer JWT.  
* **Rate limits** – 100 requests per minute per IP (configurable in `middleware/rateLimiter.ts`).  
* **Error format**  

```json
{
  "status": 400,
  "error": "ValidationError",
  "message": "Field 'amount' must be a positive number."
}
```

---

## Contributing  

We welcome contributions! Please follow these steps:

1. **Fork** the repository and **clone** your fork.  
2. Create a feature branch: `git checkout -b feat/awesome-feature`.  
3. Install dependencies (see *Getting Started*).  
4. Write tests for any new functionality.  
5. Ensure lint & format pass: `pnpm lint && pnpm format`.  
6. Commit with a clear message and push to your fork.  
7. Open a **Pull Request** against `main`.  

### Development workflow  

| Branch | Purpose |
|--------|---------|
| `main` | Stable releases (tagged). |
| `dev`  | Integration branch – PRs are merged here first. |
| `feature/*` | Individual feature work. |
| `hotfix/*` | Emergency patches to `main`. |

### Code review guidelines  

* All PRs must pass CI (lint, tests, type‑check).  
* Keep changes atomic – one logical change per PR.  
* Update documentation (README, Swagger, inline comments) when adding public APIs.  

---

## Troubleshooting  

| Issue | Solution |
|-------|----------|
| **Cannot connect to PostgreSQL** | Verify `DATABASE_URL` is correct, container is running (`docker ps`), and port `5432` is open. |
| **JWT verification fails** | Ensure the same `JWT_SECRET` is used in both client `.env` (if you proxy) and server `.env`. |
| **Vite dev server shows “Failed to load source map”** | Run `pnpm clean && pnpm dev` to clear caches. |
| **CORS errors** | The server uses `cors` middleware; make sure `origin` in `.env` matches the client URL. |
| **Docker compose hangs** | Remove stale volumes: `docker compose down -v` then `docker compose up -d`. |
| **Recurring transaction not triggering** | Check the `frequency
