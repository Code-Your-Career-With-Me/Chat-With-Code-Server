# 📄 Chat with Code — Server (API)

**Date:** 2025-08-12

A **TypeScript Node.js/Express** backend for **Chat with Code**, a random one-to-one video/audio chat web app with live text, a room system, and realtime presence via **Socket.IO**.  
Authentication (email/OTP or email/password) and session data are stored in **MongoDB**.  
WebRTC signaling is handled over **Socket.IO**.

> This repository contains the **server** half of the MERN stack project (MongoDB, Express, React, Node).  
> The **client** (React + Vite + Tailwind + TypeScript) lives in a separate repository.

---

## 🛠 Tech Stack

- **Node.js** + **Express** (TypeScript)
- **Socket.IO** (signaling, presence, matchmaking)
- **MongoDB** + **Mongoose**
- **JWT** authentication (HTTP + Socket handshake)
- **Zod** for validation
- **dotenv** for configuration
- **Helmet**, **CORS**, **rate-limit**, **hpp**, **express-mongo-sanitize** for security
- **Winston/Pino** logging
- **Vitest** / **Jest** (choose one) + **Supertest** for testing
- **ts-node-dev** for development, **tsc** for builds
- *(Optional)* **BullMQ/Redis** (email OTP queue), **Nodemailer** (SMTP)

---

## ✨ Features

- User account creation & login (email/password; OTP optional)
- JWT access & refresh tokens
- User profile & preferences (age gate, interests/tags, mic/cam defaults)
- **Realtime matchmaking** (random & interest-based)
- **Rooms API** (private/public, re-match/skip/next)
- **WebRTC signaling** over Socket.IO (offer/answer/ICE)
- Live text chat within rooms
- Presence tracking (online/offline, typing, reconnects)
- Moderation tools (block/report endpoints, room end reasons)
- Optional audit logs

---

## 🚀 Getting Started

### 📋 Prerequisites

- **Node.js** v20+
- **MongoDB** v6+ (Atlas or local)
- *(Optional)* **Redis** v7+ (for queues/rate-limiting at scale)

---

### 📥 Installation

```bash
git clone https://github.com/your-org/chat-with-code-server.git
cd chat-with-code-server
pnpm install    # or npm install / yarn install
```

---

### ⚙️ Environment Variables

Create a `.env` file in the root directory:

```env
# Server
NODE_ENV=development
PORT=8080
CORS_ORIGIN=http://localhost:5173

# MongoDB
MONGODB_URI=mongodb://127.0.0.1:27017/chatwithcode

# JWT
JWT_ACCESS_SECRET=replace-with-strong-secret
JWT_REFRESH_SECRET=replace-with-stronger-secret
JWT_ACCESS_EXPIRES=15m
JWT_REFRESH_EXPIRES=7d

# OTP / Email (optional)
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=you@example.com
SMTP_PASS=app-password
MAIL_FROM="Chat with Code <no-reply@chatwithcode.app>"

# Redis (optional)
REDIS_URL=redis://127.0.0.1:6379

# Logging
LOG_LEVEL=info
```

---

### 📜 Scripts

```bash
pnpm dev       # Run with ts-node-dev + reload
pnpm build     # Compile TypeScript to /dist
pnpm start     # Run compiled server
pnpm test      # Run unit/integration tests
pnpm lint      # Run ESLint checks
pnpm format    # Format code with Prettier
```

---

## 📂 Project Structure

```plaintext
src/
  app.ts
  index.ts
  config/
  db/
  routes/
  controllers/
  services/
  sockets/
  middleware/
  utils/
  validations/
tests/
```

---

## 🔌 API Overview

**Base URL:** `http://localhost:8080/api`

### **Auth**
- `POST /api/auth/register` — Create a new account
- `POST /api/auth/login` — Login with email/password
- `POST /api/auth/refresh` — Refresh JWT token
- `POST /api/auth/logout` — Logout and invalidate token

### **Users**
- `GET /api/users/me` — Get logged-in user details
- `PATCH /api/users/me` — Update profile
- `POST /api/users/block` — Block another user

### **Matchmaking & Rooms**
- `POST /api/match/find` — Start matchmaking
- `POST /api/match/cancel` — Cancel matchmaking
- `POST /api/rooms/:roomId/end` — End a room

---

## 📡 Socket.IO Events

### **Client → Server**
- `match:find`
- `match:cancel`
- `room:signal:offer`
- `room:signal:answer`
- `room:signal:ice`
- `room:message`

### **Server → Client**
- `match:found`
- `match:timeout`
- `room:ready`
- `room:ended`
- `room:message`

---

## 🛡 Security

- **Helmet** for HTTP headers
- **CORS** origin restrictions
- **JWT** rotation for sessions
- **Socket.IO** authentication middleware
- **Rate-limiting** for sensitive endpoints

---

## 🧪 Testing

- **Unit Tests**: Vitest or Jest
- **Integration Tests**: Supertest
- **Socket Tests**: socket.io-client

---

## 🚢 Deployment

- Dockerfile + docker-compose setup
- PM2 or systemd process management
- HTTPS via Nginx or Caddy

---

## 📜 License

MIT (or your choice)

