![Budgenix Banner](https://via.placeholder.com/1200x200/007bff/ffffff?text=Budgenix+-+Smart+Financials)

# Budgenix: Your AI-Powered Financial Companion

[![Build Status](https://img.shields.io/badge/build-passing-brightgreen)](https://github.com/kaihere14/Budgenix/actions)
[![Client Version](https://img.shields.io/badge/client_version-0.0.0-blue)](./client/package.json)
[![Server Version](https://img.shields.io/badge/server_version-1.0.0-blue)](./server/package.json)
[![License](https://img.shields.io/badge/license-ISC-blue)](LICENSE)
[![GitHub Issues](https://img.shields.io/github/issues/kaihere14/Budgenix)](https://github.com/kaihere14/Budgenix/issues)

## 🚀 Overview

Budgenix is a full-stack financial management application designed to help individuals and teams track expenses, gain insights, and collaborate effectively. Leveraging the power of AI (Google Gemini) for smart financial analysis and real-time communication (Agora RTC SDK) for collaborative features, Budgenix aims to make budgeting and financial planning intuitive and engaging.

**Key Value Proposition**: Simplify your financial life with AI-driven insights and seamless collaboration, all within a modern and user-friendly interface.

**Target Audience**: Individuals, small teams, and families looking for a comprehensive tool to manage shared or personal finances with advanced features.

**Current Status**: This project is under active development. The core functionalities for user management, expense tracking, and AI integrations are being established.

## ✨ Features

Budgenix offers a robust set of features to empower your financial journey:

*   **User Authentication**: Secure user registration, login, and session management using JWT.
*   **Expense Tracking**:
    *   Record and categorize expenses.
    *   View expense history and summaries.
    *   (Planned) Budget creation and monitoring.
*   **AI-Powered Insights (Gemini)**:
    *   Analyze spending patterns.
    *   Generate personalized financial advice.
    *   Answer financial queries using natural language.
*   **Real-time Collaboration (Agora)**:
    *   (Planned) Voice/video calls for financial discussions.
    *   (Planned) Screen sharing for collaborative budgeting sessions.
*   **Modern User Interface**: Intuitive and responsive design built with React, Tailwind CSS, DaisyUI, and Tremor for data visualization.
*   **Robust Backend**: Scalable API built with Node.js, Express, and MongoDB.
*   **Email Notifications**: (Planned) Transaction alerts, budget warnings, or summary reports via Resend.

## 🛠️ Tech Stack

Budgenix is built using a modern and powerful technology stack:

### Client (Frontend)

*   **Framework**: [React 19](https://react.dev/) - A JavaScript library for building user interfaces.
*   **Build Tool**: [Vite](https://vitejs.dev/) - Next-generation frontend tooling.
*   **Language**: [TypeScript](https://www.typescriptlang.org/) - Superset of JavaScript that adds static types.
*   **Styling**:
    *   [Tailwind CSS](https://tailwindcss.com/) - A utility-first CSS framework.
    *   [DaisyUI](https://daisyui.com/) - Tailwind CSS component library.
    *   [Tremor](https://www.tremor.so/) - React components for building dashboards.
*   **Real-time Communication**: [Agora RTC SDK NG](https://docs.agora.io/en/video-call-quickstart-web-ng/get-started) - For voice and video calling capabilities.
*   **HTTP Client**: [Axios](https://axios-http.com/) - Promise-based HTTP client.
*   **Routing**: [React Router DOM](https://reactrouter.com/en/main) - Declarative routing for React.
*   **Notifications**: [React Hot Toast](https://react-hot-toast.com/) - Lightweight and customizable toast notifications.

### Server (Backend)

*   **Runtime**: [Node.js](https://nodejs.org/en) - JavaScript runtime built on Chrome's V8 JavaScript engine.
*   **Framework**: [Express.js 5](https://expressjs.com/) - Fast, unopinionated, minimalist web framework for Node.js.
*   **Language**: [TypeScript](https://www.typescriptlang.org/) - Superset of JavaScript that adds static types.
*   **Database**: [MongoDB](https://www.mongodb.com/) - NoSQL document database.
*   **ORM/ODM**: [Mongoose](https://mongoosejs.com/) - MongoDB object modeling for Node.js.
*   **AI Integration**:
    *   [@google/generative-ai](https://ai.google.dev/gemini-api/docs/get-started/node) - Official Google Gemini API client for Node.js.
*   **Authentication**:
    *   [Bcrypt](https://www.npmjs.com/package/bcrypt) - For hashing passwords.
    *   [JSON Web Token (JWT)](https://jwt.io/) - For secure API authentication.
*   **Email Service**: [Resend](https://resend.com/) - For sending transactional emails.
*   **Utilities**:
    *   [CORS](https://www.npmjs.com/package/cors) - Middleware for enabling Cross-Origin Resource Sharing.
    *   [Dotenv](https://www.npmjs.com/package/dotenv) - Loads environment variables from a `.env` file.
    *   [Cookie-parser](https://www.npmjs.com/package/cookie-parser) - Parse Cookie header and populate `req.cookies`.

## 🏛️ Architecture

Budgenix follows a client-server architecture, organized as a monorepo:

```
.
├── client/          # React frontend application
│   ├── public/      # Static assets
│   └── src/         # React components, pages, context, hooks
│       ├── components/
│       ├── context/
│       ├── hooks/
│       └── pages/
└── server/          # Node.js/Express backend API
    └── src/         # Server source code
        ├── controllers/ # Request handlers
        ├── databases/   # Database connection logic
        ├── middleware/  # Express middleware
        ├── models/      # Mongoose schemas and models
        ├── routes/      # API route definitions
        └── types/       # TypeScript type definitions
```

**High-Level Design**:

*   **Frontend (Client)**: A single-page application (SPA) built with React. It communicates with the backend API to fetch and send data.
*   **Backend (Server)**: A RESTful API built with Express.js. It handles user authentication, data storage (MongoDB), and integrates with external services like Google Gemini and Agora.
*   **Data Flow**:
    1.  The client sends HTTP requests (GET, POST, PUT, DELETE) to the server's API endpoints.
    2.  The server processes these requests, interacts with the MongoDB database via Mongoose, and potentially calls external APIs (Gemini for AI, Agora for token generation).
    3.  The server sends back JSON responses to the client.

## 🚀 Getting Started

Follow these instructions to set up and run Budgenix on your local machine.

### Prerequisites

Before you begin, ensure you have the following installed:

*   **Node.js**: [LTS version](https://nodejs.org/en/download/) (v18.x or higher recommended)
*   **pnpm**: [Package manager](https://pnpm.io/installation) (or npm/yarn)
*   **MongoDB**:
    *   [Local installation](https://docs.mongodb.com/manual/installation/)
    *   Or a cloud-hosted service like [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
*   **Google Gemini API Key**: Obtain one from [Google AI Studio](https://aistudio.google.com/app/apikey).
*   **Agora.io Developer Account & App Credentials**:
    *   [Register on Agora.io](https://console.agora.io/signup)
    *   Create a new project to get an `App ID` and `App Certificate`.
*   **Resend API Key**: (Optional, for email features) Obtain one from [Resend](https://resend.com/).

### Installation

1.  **Clone the repository**:

    ```bash
    git clone https://github.com/kaihere14/Budgenix.git
    cd Budgenix
    ```

2.  **Install Client Dependencies**:

    ```bash
    cd client
    pnpm install # or npm install or yarn install
    cd ..
    ```

3.  **Install Server Dependencies**:

    ```bash
    cd server
    pnpm install # or npm install or yarn install
    cd ..
    ```

### Configuration

Create a `.env` file in the `server/` directory and populate it with your environment variables.

```env
# Server Configuration
PORT=3300 # Or any other port you prefer

# MongoDB
MONGO_URI="mongodb://localhost:27017/budgenix" # Replace with your MongoDB connection string

# JWT Secret for authentication
JWT_SECRET="your_jwt_secret_key" # IMPORTANT: Use a strong, random key in production

# Google Gemini AI
GEMINI_API_KEY="your_google_gemini_api_key"

# Agora.io for real-time communication
AGORA_APP_ID="your_agora_app_id"
AGORA_APP_CERTIFICATE="your_agora_app_certificate" # Used for generating RTC tokens

# Resend for email services (Optional)
RESEND_API_KEY="your_resend_api_key"
```

### Running the Application

1.  **Start the MongoDB server** (if running locally).

2.  **Start the Backend Server**:
    Open a new terminal, navigate to the `server/` directory, and run:

    ```bash
    cd server
    pnpm dev # Uses tsx to watch for changes and restart
    ```
    The server should start on the port specified in your `.env` file (default: `3300`). You should see a message like `Server running on port 3300`.

3.  **Start the Frontend Client**:
    Open another new terminal, navigate to the `client/` directory, and run:

    ```bash
    cd client
    pnpm dev
    ```
    The client application will typically open in your browser at `http://localhost:5173` (or another port if 5173 is in use).

You should now have both the frontend and backend running, ready for development and testing!

## 💡 Usage

Once both the client and server are running:

1.  **Access the application**: Open your web browser and navigate to `http://localhost:5173`.
2.  **Register/Login**: Create a new user account or log in with existing credentials.
3.  **Track Expenses**: Navigate to the expense management section to add, view, and categorize your financial transactions.
4.  **Interact with AI**: Explore the AI features to get insights or ask questions about your finances.
5.  **Collaborate**: (Once implemented) Utilize real-time communication features for shared financial planning.

## 🧑‍💻 Development

### Setting up Development Environment

The `pnpm dev` commands for both client and server provide hot-reloading/restarting capabilities for a smooth development workflow.

### Running Tests

*   **Client**:
    Currently, there are no specific test scripts defined in `client/package.json`. You would typically use a framework like Jest or React Testing Library.
*   **Server**:
    The `server/package.json` has a placeholder `test` script. You would integrate a testing framework like Jest or Mocha/Chai.

    ```bash
    cd server
    pnpm test # Currently outputs "Error: no test specified"
    ```

### Code Style Guidelines

*   **Client**: ESLint is configured for code linting.
    ```bash
    cd client
    pnpm lint
    ```
*   **Server**: TypeScript compiler is used for type checking.
    ```bash
    cd server
    pnpm type-check
    ```
    Adhere to standard TypeScript and JavaScript best practices.

### Debugging Tips

*   **Client**: Use your browser's developer tools (F12) to inspect components, network requests, and console logs.
*   **Server**: Use `console.log` statements or integrate a debugger like `ndb` or VS Code's built-in debugger with `nodemon` or `tsx`.

## 📦 Deployment

### Client (Frontend)

The client is configured for deployment with Vercel (see `client/vercel.json`).

1.  **Build**:
    ```bash
    cd client
    pnpm build
    ```
    This will create a `dist/` directory with optimized static assets.
2.  **Deploy**:
    *   Push your code to a Git repository (e.g., GitHub).
    *   Connect your repository to Vercel, and it will automatically detect the Vite project and deploy it.

### Server (Backend)

The server can be deployed to any Node.js hosting platform (e.g., Render, Railway, Heroku, AWS EC2, DigitalOcean Droplets).

1.  **Build**:
    ```bash
    cd server
    pnpm build
    ```
    This compiles TypeScript to JavaScript, outputting to the `dist/` directory.
2.  **Start Production Server**:
    ```bash
    cd server
    pnpm start
    ```
    This command runs the compiled JavaScript code.
3.  **Environment Variables**: Ensure all necessary environment variables (`MONGO_URI`, `JWT_SECRET`, `GEMINI_API_KEY`, `AGORA_APP_ID`, `AGORA_APP_CERTIFICATE`, `RESEND_API_KEY`) are configured in your hosting environment.

## 📞 API Documentation

The Budgenix backend exposes a RESTful API. Below are the main routes:

**Base URL**: `http://localhost:3300/api` (or your deployed server URL)

### Health Check

*   `GET /api/health`
    *   **Description**: Checks the server's health status.
    *   **Response**:
        ```json
        {
          "status": "ok",
          "timestamp": "2023-10-27T10:00:00.000Z"
        }
        ```

### User Management (`/api/users`)

*   `POST /api/users/register`
    *   **Description**: Registers a new user.
    *   **Request Body**: `{ "username": "...", "email": "...", "password": "..." }`
    *   **Response**: `{ "message": "User registered successfully", "user": { "id": "...", "username": "...", "email": "..." } }`
*   `POST /api/users/login`
    *   **Description**: Logs in a user.
    *   **Request Body**: `{ "email": "...", "password": "..." }`
    *   **Response**: `{ "message": "Login successful", "token": "...", "user": { "id": "...", "username": "...", "email": "..." } }`
*   *(Other user-related routes like `GET /api/users/:id`, `PUT /api/users/:id` would be implemented here)*

### Expense Management (`/api/expenses`)

*   `POST /api/expenses`
    *   **Description**: Adds a new expense. (Requires authentication)
    *   **Request Body**: `{ "amount": 50.00, "category": "Food", "description": "Lunch", "date": "2023-10-27" }`
    *   **Response**: `{ "message": "Expense added", "expense": { ... } }`
*   `GET /api/expenses`
    *   **Description**: Retrieves all expenses for the authenticated user. (Requires authentication)
    *   **Response**: `[ { ...expense1 }, { ...expense2 } ]`
*   *(CRUD operations for expenses: `GET /api/expenses/:id`, `PUT /api/expenses/:id`, `DELETE /api/expenses/:id`)*

### Agora (Real-time Communication) (`/api/agora`)

*   `POST /api/agora/token`
    *   **Description**: Generates an Agora RTC token for joining a video/audio channel.
    *   **Request Body**: `{ "channelName": "my-budget-session", "uid": 0 }` (UID 0 for random, or specific user ID)
    *   **Response**: `{ "rtcToken": "..." }`

### Gemini AI Integration (`/api/gemini`)

*   `POST /api/gemini/chat`
    *   **Description**: Sends a query to the Gemini AI and gets a response.
    *   **Request Body**: `{ "message": "What are some tips for saving money on groceries?" }`
    *   **Response**: `{ "response": "..." }`

**Authentication**: Most API endpoints (except `/register`, `/login`, `/health`) require a JSON Web Token (JWT) in the `Authorization` header as a Bearer token.

```
Authorization: Bearer <your_jwt_token>
```

## 🤝 Contributing

We welcome contributions to Budgenix! If you're interested in improving the project, please follow these guidelines:

1.  **Fork the repository**: Click the "Fork" button at the top right of this page.
2.  **Clone your forked repository**:
    ```bash
    git clone https://github.com/YOUR_USERNAME/Budgenix.git
    cd Budgenix
    ```
3.  **Create a new branch**:
    ```bash
    git checkout -b feature/your-feature-name
    ```
4.  **Make your changes**: Implement your feature or fix bugs.
5.  **Commit your changes**: Write clear and concise commit messages.
    ```bash
    git commit -m "feat: Add new expense categorization"
    ```
6.  **Push to your fork**:
    ```bash
    git push origin feature/your-feature-name
    ```
7.  **Open a Pull Request**: Go to the original Budgenix repository on GitHub and open a new pull request from your forked branch.

### Development Workflow

*   Ensure your code adheres to the existing code style and passes linting/type-checking.
*   Write tests for new features or bug fixes where applicable.
*   Provide a clear description of your changes in the pull request.

## ⁉️ Troubleshooting

*   **`pnpm install` errors**: Ensure you have Node.js and pnpm installed correctly. Try clearing the cache (`pnpm cache clean --force`).
*   **Server not starting**:
    *   Check your `.env` file for correct variable names and values (especially `MONGO_URI`, `PORT`).
    *   Ensure MongoDB is running if you're using a local instance.
    *   Check the console for error messages.
*   **Client not connecting to server**:
    *   Verify the server is running on the expected port.
    *   Check network requests in your browser's developer tools for failed API calls (CORS issues, incorrect endpoint URLs).
*   **CORS errors**: Ensure your server's `cors` configuration allows requests from your client's origin (`http://localhost:5173` during development).
*   **AI/Agora errors**: Double-check your `GEMINI_API_KEY`, `AGORA_APP_ID`, and `AGORA_APP_CERTIFICATE` in the `server/.env` file.

**Where to get help**: If you encounter persistent issues, please open an issue on the [GitHub Issues page](https://github.com/kaihere14/Budgenix/issues).

## 🗺️ Roadmap

Here are some planned features and future enhancements for Budgenix:

*   **Advanced Budgeting**: Create custom budgets, track progress, and receive alerts.
*   **Reporting & Analytics**: Generate detailed reports and visualizations of spending habits.
*   **Multi-user Accounts**: Support for shared finances and collaborative expense tracking within a group.
*   **Transaction Import**: Integrate with banking APIs or allow CSV imports for transactions.
*   **Mobile Application**: Develop native iOS/Android apps.
*   **Notifications**: Implement email and in-app notifications for financial events.
*   **Improved AI Features**: More sophisticated financial forecasting and scenario planning.

## 📄 License & Credits

This project is licensed under the **ISC License**. See the [LICENSE](LICENSE) file for details.

### Contributors

*   [kaihere14](https://github.com/kaihere14) - Initial project setup and core development.

### Acknowledgments

*   Thanks to all the open-source projects and libraries that make Budgenix possible.
*   Special thanks to Google for the Gemini API and Agora.io for their real-time communication SDK.