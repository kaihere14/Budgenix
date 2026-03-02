# Budgenix: Your AI-Powered Personal Finance Manager

[![License: ISC](https://img.shields.io/badge/License-ISC-blue.svg)](https://opensource.org/licenses/ISC)
[![Client Version](https://img.shields.io/badge/client-v0.0.0-blue.svg)](./client/package.json)
[![Server Version](https://img.shields.io/badge/server-v1.0.0-blue.svg)](./server/package.json)
<!-- Add more badges as project matures: Build Status, Test Coverage, etc. -->

## 🚀 Overview

Budgenix is a full-stack personal finance management application designed to help you effortlessly track your expenses, manage your income, and gain insightful financial advice through an intuitive AI conversational agent. Leveraging the power of modern web technologies and advanced AI, Budgenix provides a seamless experience for budgeting and understanding your financial health.

**Key Value Proposition**: Stop guessing about your finances. Budgenix empowers you with clear expense tracking and personalized, real-time financial guidance from an AI assistant, making budgeting accessible and actionable.

**Target Audience**: Individuals seeking to improve their personal finance management, track spending habits, and receive intelligent, conversational advice on their financial decisions.

**Current Status**: This project is currently in active development, focusing on establishing core expense tracking and AI integration features.

## ✨ Features

*   **User Authentication**: Secure user registration and login.
*   **Expense Tracking**:
    *   Record and categorize daily expenses.
    *   View a comprehensive list of all your expenditures.
    *   Summarize spending by category and overall.
*   **Income Management**: Track your income to understand your remaining balance.
*   **AI Conversational Budget Assistant**:
    *   **Real-time Voice Interaction**: Engage with an AI agent for financial advice using natural language.
    *   **Personalized Insights**: Receive summaries of your spending, remaining balance, and category-wise expenditures.
    *   **Smart Advice**: Get practical recommendations on potential purchases based on your current financial situation.
    *   **Powered by Agora & Gemini**: Utilizes Agora's Conversational AI Agent for voice interaction and Google Gemini for intelligent financial analysis.
*   **Intuitive User Interface**: Built with React, TailwindCSS, DaisyUI, and Tremor for a modern and responsive experience.

## 🛠️ Tech Stack

Budgenix is built as a monorepo with a robust technology stack for both frontend and backend.

### Frontend (Client)

*   **Framework**: [React.js](https://react.dev/) (with [Vite](https://vitejs.dev/) for fast development)
*   **Styling**: [Tailwind CSS](https://tailwindcss.com/) & [DaisyUI](https://daisyui.com/)
*   **Components**: [Tremor](https://www.tremor.so/) for data visualization and UI components.
*   **AI Integration**: [Agora RTC SDK NG](https://www.agora.io/en/products/interactive-live-streaming/) for real-time voice communication with the AI agent.
*   **HTTP Client**: [Axios](https://axios-http.com/)
*   **Routing**: [React Router DOM](https://reactrouter.com/en/main)
*   **Notifications**: [React Hot Toast](https://react-hot-toast.com/)
*   **Icons**: [Lucide React](https://lucide.dev/icons/)

### Backend (Server)

*   **Runtime**: [Node.js](https://nodejs.org/)
*   **Framework**: [Express.js](https://expressjs.com/)
*   **Language**: [TypeScript](https://www.typescriptlang.org/)
*   **Database ORM**: [Mongoose](https://mongoosejs.com/)
*   **Authentication**: [JSON Web Tokens (JWT)](https://jwt.io/) & [Bcrypt](https://www.npmjs.com/package/bcrypt)
*   **Environment Variables**: [Dotenv](https://www.npmjs.com/package/dotenv)
*   **CORS**: [CORS](https://www.npmjs.com/package/cors) middleware
*   **Email Service**: [Resend](https://resend.com/) (for potential future features like password resets or notifications)
*   **AI Integration**:
    *   [Google Generative AI](https://ai.google.dev/): For powering the LLM capabilities of the financial assistant.
    *   [Agora Conversational AI Agent](https://www.agora.io/en/products/conversational-ai-agent/): Manages the voice interaction, ASR (Automatic Speech Recognition), and TTS (Text-to-Speech).

### Database

*   **NoSQL Database**: [MongoDB](https://www.mongodb.com/)

## 🏗️ Architecture

Budgenix follows a client-server architecture organized within a monorepo structure:

```
.
├── client/          # Frontend React application
└── server/          # Backend Node.js/Express API
```

### Client Architecture

The `client/` directory contains a standard React application bootstrapped with Vite.
*   `src/pages/`: Top-level views of the application.
*   `src/components/`: Reusable UI components.
*   `src/context/`: React Context for global state management.
*   `src/hooks/`: Custom React hooks for encapsulating logic.

### Server Architecture

The `server/` directory hosts the Node.js/Express API written in TypeScript.
*   `src/index.ts`: The main entry point, responsible for initializing the Express app, connecting to MongoDB, and registering routes.
*   `src/routes/`: Defines API endpoints for different resources (users, expenses, Agora AI, Gemini AI).
*   `src/controllers/`: Contains the business logic for handling requests and interacting with models and external services. The `agora.controller.ts` is central to the AI functionality, orchestrating communication with Agora and Gemini.
*   `src/models/`: Mongoose schemas defining the structure of data stored in MongoDB (e.g., `User`, `Expense`).
*   `src/databases/`: Handles the connection to the MongoDB database.
*   `src/middleware/`: Contains middleware functions, likely for authentication and authorization.

### Data Flow

1.  The **Client** (React app) sends HTTP requests to the **Server** (Express API).
2.  The **Server** processes these requests:
    *   For user and expense management, it interacts with **MongoDB** via Mongoose.
    *   For AI interactions:
        *   It retrieves the user's financial summary from **MongoDB**.
        *   It then makes requests to the **Agora Conversational AI Agent** API, injecting the user's financial data and configuring the Gemini LLM.
        *   Agora handles the real-time voice (ASR/TTS) and forwards text prompts to **Google Gemini** (proxied through the server) for financial analysis based on the provided summary.
        *   Agora then converts Gemini's text responses back into speech for the client.
3.  The **Server** sends responses back to the **Client**, which then updates the UI.

## 🚀 Getting Started

Follow these instructions to set up and run Budgenix on your local machine.

### Prerequisites

Ensure you have the following software installed:

*   **Node.js**: v18.x or higher (LTS recommended)
*   **pnpm**: v8.x or higher (recommended for monorepo, or npm v9.x+)
*   **MongoDB**: A running instance of MongoDB (local or cloud-hosted like MongoDB Atlas).

#### API Keys & Accounts

You will need accounts and API keys for the following services:

*   **Agora.io Developer Account**:
    *   `AGORA_APP_ID`
    *   `AGORA_CUSTOMER_ID`
    *   `AGORA_CUSTOMER_SECRET`
    *   `AGORA_AGENT_TOKEN` (for Conversational AI Agent)
*   **Google Cloud Project**:
    *   Enable the Gemini API.
    *   `GEMINI_API_KEY_SECOND` (Your Google Gemini API Key)
*   **Azure Cognitive Services Account**:
    *   `AZURE_TTS_KEY` (for Text-to-Speech)
    *   `AZURE_TTS_REGION` (e.g., `eastus`)

### Installation

1.  **Clone the repository**:

    ```bash
    git clone https://github.com/kaihere14/Budgenix.git
    cd Budgenix
    ```

2.  **Install dependencies for both client and server**:

    ```bash
    # Install server dependencies
    cd server
    pnpm install # or npm install
    cd ..

    # Install client dependencies
    cd client
    pnpm install # or npm install
    cd ..
    ```

### Configuration

Create `.env` files in both the `server/` and `client/` directories based on the examples below.

#### Server Configuration (`server/.env`)

```env
PORT=3300
MONGO_URI="mongodb://localhost:27017/budgenix" # Replace with your MongoDB connection string
JWT_SECRET="your_jwt_secret_key" # Use a strong, random string
AGORA_APP_ID="YOUR_AGORA_APP_ID"
AGORA_CUSTOMER_ID="YOUR_AGORA_CUSTOMER_ID"
AGORA_CUSTOMER_SECRET="YOUR_AGORA_CUSTOMER_SECRET"
AGORA_AGENT_TOKEN="YOUR_AGORA_AGENT_TOKEN"
GEMINI_API_KEY_SECOND="YOUR_GEMINI_API_KEY"
AZURE_TTS_KEY="YOUR_AZURE_TTS_KEY"
AZURE_TTS_REGION="eastus" # e.g., eastus, westus, etc.
```

#### Client Configuration (`client/.env`)

```env
VITE_SERVER_URL="http://localhost:3300/api" # Adjust if your server runs on a different port
```

## 🏃 Usage

1.  **Start the Backend Server**:

    Navigate to the `server/` directory and run:

    ```bash
    cd server
    pnpm dev # or npm run dev
    ```

    The server should start on `http://localhost:3300` (or your specified `PORT`). You'll see a message like `Server running on port 3300`.

2.  **Start the Frontend Application**:

    Navigate to the `client/` directory and run:

    ```bash
    cd client
    pnpm dev # or npm run dev
    ```

    The client application will open in your browser, usually at `http://localhost:5173` (or a similar Vite development URL).

3.  **Interact with Budgenix**:
    *   Register a new user account or log in.
    *   Start adding your expenses and income.
    *   Look for the AI assistant interface to start a conversation about your finances.

## ⚙️ Development

### Setting up Development Environment

*   Ensure all prerequisites and installation steps are completed.
*   Use `pnpm dev` in both `client/` and `server/` directories to run development servers with hot-reloading.

### Running Tests

*(Currently, there are no explicit test scripts defined in `package.json` for either client or server. This section is a placeholder for future test implementation.)*

```bash
# Example: To run client tests (if configured)
cd client
pnpm test

# Example: To run server tests (if configured)
cd server
pnpm test
```

### Code Style

The client uses ESLint for code linting. You can run it with:

```bash
cd client
pnpm lint # or npm run lint
```

## ☁️ Deployment

### Building for Production

1.  **Build the Server**:

    ```bash
    cd server
    pnpm build # or npm run build
    ```

    This will compile TypeScript files to JavaScript in the `dist/` directory.

2.  **Build the Client**:

    ```bash
    cd client
    pnpm build # or npm run build
    ```

    This will create a production-ready build in the `client/dist/` directory.

### Running in Production

After building, you can start the server in production mode:

```bash
cd server
pnpm start # or npm start
```

For the client, the `client/dist/` folder can be served by any static file server or deployed to a platform like Vercel (as indicated by `vercel.json`).

## 📞 API Documentation

The Budgenix backend exposes a RESTful API.

### Base URL

`http://localhost:3300/api` (or your configured server URL)

### Authentication

Most endpoints require a JSON Web Token (JWT) passed in the `Authorization` header as a Bearer token.

`Authorization: Bearer <your_jwt_token>`

### Endpoints

#### User Management

*   `POST /api/users/register`: Register a new user.
*   `POST /api/users/login`: Authenticate a user and receive a JWT.
*   `GET /api/users/profile`: Get the authenticated user's profile. (Requires JWT)

#### Expense Management

*   `POST /api/expenses`: Add a new expense. (Requires JWT)
*   `GET /api/expenses`: Retrieve all expenses for the authenticated user. (Requires JWT)
*   `GET /api/expenses/:id`: Retrieve a specific expense by ID. (Requires JWT)
*   `PUT /api/expenses/:id`: Update an existing expense. (Requires JWT)
*   `DELETE /api/expenses/:id`: Delete an expense. (Requires JWT)

#### AI Conversational Agent

These endpoints interact with the Agora Conversational AI Agent.

*   `POST /api/agora/start-ai`
    *   **Description**: Initiates the AI budget manager agent for a user. It fetches the user's financial summary and configures the Agora agent with Google Gemini for LLM capabilities and Azure for TTS.
    *   **Authentication**: Requires JWT.
    *   **Request Body**:
        ```json
        {
            "channel": "convai_nVwXMR" // The Agora channel name to join
        }
        ```
    *   **Response**: Contains Agora agent details if successful.
*   `POST /api/agora/stop-ai`
    *   **Description**: Terminates a running AI agent instance.
    *   **Authentication**: Requires JWT.
    *   **Request Body**:
        ```json
        {
            "agent_id": "YOUR_AGENT_ID" // The ID of the agent to stop, received from start-ai response
        }
        ```
    *   **Response**: Confirmation of agent termination.
*   `POST /api/agora/callback`
    *   **Description**: This is a webhook endpoint configured with Agora.io to receive real-time events from the Conversational AI Agent (e.g., ASR results, LLM replies, TTS status). It is not meant to be called directly by the client.
    *   **Request Body**: Agora event payload.
    *   **Response**: `200 OK`

#### Gemini AI (Direct Proxy)

*   `POST /api/gemini/chat`
    *   **Description**: A direct proxy to the Google Gemini API for general chat interactions. (Details on request/response format would depend on implementation).
    *   **Authentication**: Requires JWT.

## 🤝 Contributing

We welcome contributions to Budgenix! If you're interested in improving the project, please follow these guidelines:

1.  **Fork the repository**.
2.  **Create a new branch** for your feature or bug fix: `git checkout -b feature/your-feature-name` or `bugfix/issue-description`.
3.  **Make your changes**.
4.  **Commit your changes** with a clear and descriptive message.
5.  **Push your branch** to your forked repository.
6.  **Open a Pull Request** to the `main` branch of the original repository.

Please ensure your code adheres to the existing code style and passes any linting checks.

## ❓ Troubleshooting

*   **Missing Environment Variables**: Double-check that all required `.env` variables are set correctly in both `server/.env` and `client/.env`.
*   **MongoDB Connection Issues**: Ensure your MongoDB instance is running and accessible, and that your `MONGO_URI` in `server/.env` is correct.
*   **AI Agent Errors**: Verify all Agora, Gemini, and Azure API keys/secrets are correct and that the services are enabled for your accounts. Check the server logs for detailed error messages from the Agora API.
*   **CORS Errors**: Ensure the `client/.env` `VITE_SERVER_URL` matches the server's origin, and that the server's CORS configuration allows requests from your client's URL.

If you encounter persistent issues, please open an issue on the GitHub repository.

## 🗺️ Roadmap

*   **Enhanced Data Visualizations**: More comprehensive charts and graphs for spending patterns and financial trends using Tremor.
*   **Budget Planning**: Tools for setting budgets for different categories and tracking progress.
*   **Financial Goal Setting**: Features to define and track savings goals.
*   **Mobile Application**: Native mobile apps for iOS and Android.
*   **Advanced AI Capabilities**: More proactive financial advice, anomaly detection in spending, and personalized recommendations.

## 📄 License & Credits

This project is licensed under the ISC License - see the [LICENSE](https://opensource.org/licenses/ISC) file for details.

### Contributors

*   [kaihere14](https://github.com/kaihere14) - Initial development and core features.

### Acknowledgments

*   Thanks to Agora.io for their powerful Conversational AI Agent.
*   Thanks to Google for the Gemini API.
*   Thanks to Azure for their Text-to-Speech services.
*   Thanks to the creators of React, Node.js, Express, MongoDB, and all other open-source libraries used in this project.