# Budgenix (FinBuddy)  

![Build Status](https://img.shields.io/github/actions/workflow/status/kaihere14/Budgenix/ci.yml?branch=main&label=CI) ![License](https://img.shields.io/github/license/kaihere14/Budgenix) ![Version](https://img.shields.io/github/package-json/v/kaihere14/Budgenix)  

**Budgenix** (aka *FinBuddy*) is a full‑stack personal finance assistant that lets users track expenses, manage budgets, and get AI‑powered insights in real‑time. The web client is built with React + Vite, TailwindCSS and daisyUI, while the backend is a TypeScript‑powered Express API backed by MongoDB. Integrated AI services (Google Gemini & Agora) provide smart expense categorisation, budgeting recommendations, and conversational assistance.

---

## Table of Contents  

- [Features](#features)  
- [Tech Stack](#tech-stack)  
- [Architecture Overview](#architecture-overview)  
- [Getting Started](#getting-started)  
  - [Prerequisites](#prerequisites)  
  - [Installation](#installation)  
  - [Running the Development Environment](#running-the-development-environment)  
- [Usage](#usage)  
  - [Client](#client)  
  - [Server API](#server-api)  
- [Development](#development)  
- [Deployment](#deployment)  
- [API Reference](#api-reference)  
- [Contributing](#contributing)  
- [Roadmap](#roadmap)  
- [Troubleshooting & FAQ](#troubleshooting--faq)  
- [License & Credits](#license--credits)  

---

## Features  

| Category | Feature | Status |
|----------|---------|--------|
| **Authentication** | Secure sign‑up / login with bcrypt‑hashed passwords and JWT‑based sessions | ✅ Stable |
| **Expense Management** | CRUD endpoints for expenses, automatic categorisation via Gemini AI | ✅ Stable |
| **Budgeting** | Set monthly budgets, visual dashboards (Tremor charts) | ✅ Stable |
| **AI Assistant** | Real‑time conversational assistance using Agora RTC and Gemini for suggestions | 🧪 Beta |
| **Email Notifications** | Transactional emails (welcome, password reset) via Resend | ✅ Stable |
| **Responsive UI** | TailwindCSS + daisyUI components, mobile‑first design | ✅ Stable |
| **Real‑time Collaboration** | Multi‑user video/audio chat powered by Agora (future expansion) | 🧪 Beta |
| **Testing & Linting** | ESLint, TypeScript strict mode, unit‑test scaffolding | ✅ Stable |

---

## Tech Stack  

| Layer | Technology | Reason |
|-------|------------|--------|
| **Client** | React 19, Vite 7, TailwindCSS 4, daisyUI, Tremor (charts), Lucide icons, React‑Router‑DOM 7, Axios, React‑Hot‑Toast | Modern, fast, and highly customisable UI |
| **Server** | Node 20, Express 5, TypeScript 5, MongoDB (Mongoose), JWT, Bcrypt, dotenv, cors, Axios | Scalable, type‑safe backend |
| **AI Services** | Google Gemini (`@google/generative-ai`), Agora RTC SDK (`agora-rtc-sdk-ng`) | Natural‑language insights & real‑time communication |
| **Email** | Resend (`resend`) | Simple transactional email delivery |
| **DevOps** | ESLint, TypeScript compiler, tsx (dev runner), nodemon, pnpm (or npm) | Fast feedback loops |
| **Containerisation (optional)** | Docker (Dockerfile not included – add as needed) | Consistent production environment |

---

## Architecture Overview  

```
root
├─ client/                # React front‑end (Vite)
│   ├─ src/
│   │   ├─ components/    # UI components (buttons, cards, etc.)
│   │   ├─ pages/         # Route‑level pages (Dashboard, Login, …)
│   │   ├─ context/       # React Context providers (auth, theme)
│   │   ├─ hooks/         # Custom hooks (useAuth, useExpenses)
│   │   └─ assets/        # Images, SVGs
│   └─ public/            # Vite static assets
│
├─ server/                # Express API (TypeScript)
│   ├─ src/
│   │   ├─ controllers/   # Business logic for users, expenses, AI, etc.
│   │   ├─ routes/        # Express routers (user.routes.ts, expense.routes.ts …)
│   │   ├─ models/        # Mongoose schemas (User, Expense)
│   │   ├─ middleware/    # Auth, error handling, validation
│   │   ├─ databases/     # MongoDB connection helper
│   │   ├─ types/         # Shared TypeScript interfaces
│   │   └─ index.ts       # App bootstrap
│   └─ tsconfig.json
│
└─ .gitignore, README.md, package.json (root only for repo metadata)
```

* **Data Flow** – The client talks to the server through a RESTful JSON API (`/api/*`). The server validates JWTs, performs DB operations, and optionally calls external AI services before responding.  
* **AI Integration** – Gemini is used for expense categorisation and budgeting advice; Agora provides real‑time voice/video streams for the chat assistant.  

---

## Getting Started  

### Prerequisites  

| Tool | Minimum Version |
|------|-----------------|
| Node.js | **20.x** |
| pnpm (recommended) or npm | latest |
| MongoDB | **6.x** (local or Atlas) |
| Git | any |
| (Optional) Docker | 20.10+ |

Create a free MongoDB Atlas cluster or run a local instance and note the connection URI.

### Installation  

```bash
# Clone the repository
git clone https://github.com/kaihere14/Budgenix.git
cd Budgenix

# Install root dependencies (none required currently)
# Install client dependencies
cd client
pnpm install   # or `npm install`

# Install server dependencies
cd ../server
pnpm install   # or `npm install`
```

### Environment Variables  

Create a `.env` file in the **server** directory:

```dotenv
# Server
PORT=3300
MONGODB_URI=mongodb+srv://<username>:<password>@cluster0.mongodb.net/budgenix?retryWrites=true&w=majority
JWT_SECRET=your_jwt_secret_here
JWT_EXPIRES_IN=7d

# AI / Third‑party
GEMINI_API_KEY=your_google_gemini_key
AGORA_APP_ID=your_agora_app_id
AGORA_APP_CERTIFICATE=your_agora_certificate

# Email (Resend)
RESEND_API_KEY=your_resend_api_key
```

> **Tip:** Keep `.env` out of version control (`.gitignore` already excludes it).

### Running the Development Environment  

```bash
# Terminal 1 – start the API server (with hot‑reloading)
cd server
pnpm dev   # runs `tsx watch src/index.ts`

# Terminal 2 – start the React client
cd ../client
pnpm dev   # runs `vite`
```

Open `http://localhost:5173` (Vite default) to view the UI. The client proxies API calls to `http://localhost:3300` (configured in `vite.config.js`).

---

## Usage  

### Client  

* **Sign‑up / Login** – Use the auth forms on the landing page. Credentials are stored securely with bcrypt on the server and a JWT is saved in `localStorage`.  
* **Dashboard** – Visualise monthly spend, budget utilisation, and AI‑generated recommendations.  
* **Add Expense** – Fill the “New Expense” form; the server will automatically assign a category using Gemini.  
* **AI Assistant** – Click the “Chat with FinBuddy” button to open a real‑time Agora session where you can ask budgeting questions.

### Server API  

All endpoints are prefixed with `/api`. The server returns JSON responses and uses standard HTTP status codes.

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| `GET` | `/api/health` | Health check – returns `{status:"ok"}` | ❌ |
| `POST` | `/api/users/register` | Register a new user (email, password) | ❌ |
| `POST` | `/api/users/login` | Authenticate and receive JWT | ❌ |
| `GET` | `/api/users/me` | Get current user profile | ✅ |
| `PUT` | `/api/users/me` | Update profile (name, email) | ✅ |
| `GET` | `/api/expenses` | List expenses for the authenticated user | ✅ |
| `POST` | `/api/expenses` | Create a new expense (amount, date, description) – AI categorisation runs automatically | ✅ |
| `PUT` | `/api/expenses/:id` | Update an expense | ✅ |
| `DELETE` | `/api/expenses/:id` | Delete an expense | ✅ |
| `POST` | `/api/gemini/insights` | Get AI‑generated budgeting insights (payload: `{expenses: [...]}`) | ✅ |
| `POST` | `/api/agora/token` | Generate an Agora RTC token for a given channel | ✅ |

**Example: Register a user**

```bash
curl -X POST http://localhost:3300/api/users/register \
  -H "Content-Type: application/json" \
  -d '{"email":"alice@example.com","password":"StrongPass!123"}'
```

**Example: Fetch expenses (with JWT)**

```bash
TOKEN=$(curl -s -X POST http://localhost:3300/api/users/login \
  -H "Content-Type: application/json" \
  -d '{"email":"alice@example.com","password":"StrongPass!123"}' | jq -r .token)

curl -H "Authorization: Bearer $TOKEN" http://localhost:3300/api/expenses
```

---

## Development  

| Task | Command |
|------|---------|
| Run server with hot‑reload | `cd server && pnpm dev` |
| Build server for production | `cd server && pnpm build` |
| Run client dev server | `cd client && pnpm dev` |
| Build client for production | `cd client && pnpm build` |
| Lint client code | `cd client && pnpm lint` |
| Type‑check server | `cd server && pnpm type-check` |

### Code Style  

* **Client** – ESLint (`@eslint/js`, `eslint-plugin-react-hooks`, `eslint-plugin-react-refresh`).  
* **Server** – TypeScript strict mode (`tsconfig.json`). Follow the existing folder conventions (`controllers`, `routes`, `models`).  

### Testing  

No test suite is shipped yet. Feel free to add Jest/Mocha for unit tests and Cypress for end‑to‑end UI tests.

---

## Deployment  

### Server  

1. Build the TypeScript source: `pnpm build` → `dist/` folder.  
2. Deploy `dist/` to any Node‑compatible host (Heroku, Railway, Render, Vercel Serverless, etc.).  
3. Ensure environment variables are set on the host.  

**Docker (optional)**  

```dockerfile
# Dockerfile (place in /server)
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY package*.json ./
RUN npm ci --production
EXPOSE 3300
CMD ["node", "dist/index.js"]
```

```bash
docker build -t budgenix-server .
docker run -d -p 3300:3300 --env-file .env budgenix-server
```

### Client  

1. `pnpm build` creates a static `dist/` folder.  
2. Deploy to Vercel, Netlify, Cloudflare Pages, or any static‑host.  
3. Set the `VITE_API_BASE_URL` environment variable (if you use one) to point to the live API endpoint.

---

## API Reference  

### Authentication  

| Endpoint | Method | Body | Response |
|----------|--------|------|----------|
| `/api/users/register` | POST | `{email:string, password:string, name?:string}` | `201 Created` – `{userId, token}` |
| `/api/users/login` | POST | `{email:string, password:string}` | `200 OK` – `{token, user}` |
| `/api/users/me` | GET | – | `200 OK` – user object |
| `/api/users/me` | PUT | `{name?, email?, password?}` | `200 OK` – updated user |

### Expenses  

| Endpoint | Method | Body | Response |
|----------|--------|------|----------|
| `/api/expenses` | GET | – | `200 OK` – array of expenses |
| `/api/expenses` | POST | `{amount:number, date:string, description:string, category?:string}` | `201 Created` – created expense (category may be auto‑filled) |
| `/api/expenses/:id` | PUT | same as POST | `200 OK` – updated expense |
| `/api/expenses/:id` | DELETE | – | `204 No Content` |

### AI  

| Endpoint | Method | Body | Response |
|----------|--------|------|----------|
| `/api/gemini/insights` | POST | `{expenses: Expense[]}` | `200 OK` – `{insights:string}` |
| `/api/agora/token` | POST | `{channel:string, uid?:number}` | `200 OK` – `{token:string, appId:string}` |

*All protected routes require an `Authorization: Bearer <jwt>` header.*

---

## Contributing  

1. **Fork** the repository.  
2. **Create a feature branch**: `git checkout -b feat/awesome-feature`.  
3. **Install dependencies** (see *Getting Started*).  
4. **Make your changes** – keep linting (`pnpm lint`) and TypeScript checks (`pnpm type-check`) clean.  
5. **Write tests** (if applicable) and ensure they pass.  
6. **Commit** with a clear message: `git commit -m "feat: add AI budgeting insights"`.  
7. **Push** to your fork and open a **Pull Request** against `main`.  

### Code Review Guidelines  

* Follow the existing folder structure.  
* Keep API contracts stable – update OpenAPI docs if you modify endpoints.  
* Add JSDoc/TSDoc comments for new functions.  
* Update the `README` if you add public‑facing features.  

---

## Roadmap  

- [ ] Full test coverage (Jest + React Testing Library).  
- [ ] OpenAPI (Swagger) documentation generation.  
- [ ] Docker‑Compose setup for local development (MongoDB + API + client).  
- [ ] Multi‑currency support.  
- [ ] Mobile app (React Native) wrapper.  
- [ ] Advanced AI: predictive cash‑flow forecasts.  

---

## Troubleshooting & FAQ  

| Issue | Solution |
|-------|----------|
| **MongoDB connection error** | Verify `MONGODB_URI` in `.env`. Ensure network access if using Atlas. |
| **CORS blocked** | The server enables `cors()` for all origins in development. For production, configure allowed origins in `server/src/middleware/cors.ts` (if you add one). |
| **JWT verification fails** | Check that `JWT_SECRET` matches between client and server and that the token is stored correctly (`localStorage`). |
| **Agora token generation returns 401** | Ensure `AGORA_APP_ID` and `AGORA_APP_CERTIFICATE` are correct and that the channel name is alphanumeric. |
| **Gemini API quota exceeded** | Upgrade your Google Cloud quota or implement request throttling. |
| **`pnpm dev` hangs** | Delete `node_modules` and reinstall (`pnpm install`). Ensure Node version ≥ 20. |

For additional help, open an issue or join the discussion in the repository’s **Discussions** tab.

---

## License & Credits  

**License:** ISC – see the `LICENSE` file.  

### Credits  

- **React** – UI library, https://react.dev  
- **TailwindCSS** – Utility‑first CSS framework, https://tailwindcss.com  
- **daisyUI** – Tailwind component library, https://daisyui.com  
- **Tremor** – Data visualisation components