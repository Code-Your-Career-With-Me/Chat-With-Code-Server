📄 Chat with Code — Server (API) README
Date: 2025-08-12

A TypeScript Node.js/Express backend for Chat with Code, a random one-to-one video/audio chat web app with live text, room system, and realtime presence via Socket.IO.
Auth (email/OTP or email/password) and session data are stored in MongoDB. WebRTC signaling is handled over Socket.IO.

This repo is the server half of a MERN stack project (MongoDB, Express, React, Node).
The client (React + Vite + Tailwind + TS) lives in a separate repo.

🛠 Tech Stack
Node.js + Express (TypeScript)

Socket.IO (signaling, presence, matchmaking)

MongoDB + Mongoose

JWT auth (HTTP + Socket handshake)

Zod for validation

dotenv for configuration

Helmet, CORS, rate-limit, hpp, express-mongo-sanitize for security

Winston/Pino logging

Vitest/Jest (pick one), Supertest for tests

ts-node-dev for dev, tsc for builds

Optional: BullMQ/Redis (email OTP queue), Nodemailer (SMTP)

✨ Features
Account creation & login (email/password; OTP optional)

JWT access & refresh tokens

Profile & preferences (age gate, interests/tags, mic/cam defaults)

Realtime Matchmaking (random & interest-based)

Rooms API (private/public, re-match/skip/next)

WebRTC Signaling over Socket.IO (offer/answer/ice)

Live Text Chat within a room

Presence (online/offline, typing, reconnects)

Moderation hooks (block/report endpoints, room end reasons)

Audit logs (optional)

🚀 Getting Started
Prerequisites
Node.js 20+

MongoDB 6+ (Atlas or local)

(Optional) Redis 7+ (for queues/rate-limits at scale)

Install
bash
Copy
Edit
git clone https://github.com/your-org/chat-with-code-server.git
cd chat-with-code-server
pnpm i  # or npm i / yarn
Env Setup
Create .env:

env
Copy
Edit
# Server
NODE_ENV=development
PORT=8080
CORS_ORIGIN=http://localhost:5173

# Mongo
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
Scripts
bash
Copy
Edit
pnpm dev       # run with ts-node-dev + reload
pnpm build     # tsc build to /dist
pnpm start     # run compiled server
pnpm test      # unit/integration tests
pnpm lint      # eslint
pnpm format    # prettier
📂 Project Structure
arduino
Copy
Edit
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
🔌 API Overview
Base URL: http://localhost:8080/api

Auth

POST /api/auth/register

POST /api/auth/login

POST /api/auth/refresh

POST /api/auth/logout

Users

GET /api/users/me

PATCH /api/users/me

POST /api/users/block

Matchmaking & Rooms

POST /api/match/find

POST /api/match/cancel

POST /api/rooms/:roomId/end

📡 Socket.IO Events
Client → Server

match:find, room:signal:offer, etc.

Server → Client

match:found, room:ready, etc.

🛡 Security
Helmet, CORS, JWT rotation

Socket auth guard

Rate limits

🧪 Testing
Unit & Integration with Vitest/Jest

Socket tests with socket.io-client

🚢 Deployment
Dockerfile + docker-compose

PM2/systemd

HTTPS via Nginx/Caddy

📜 License
MIT (or your choice).
