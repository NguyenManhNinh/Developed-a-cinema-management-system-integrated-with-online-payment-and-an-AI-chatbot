# 🎬 NMN Cinema – Cinema Management System with Online Ticketing & AI Chatbot

<p align="center">
  <img src="frontend/src/assets/images/NMN_CENIMA_LOGO.png" alt="NMN Cinema Logo" width="180"/>
</p>
<p align="center">
  <strong>A full-stack MERN cinema management and online ticket booking system with VNPay payment integration, real-time seat selection, and an AI-powered movie chatbot.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=white" alt="React"/>
  <img src="https://img.shields.io/badge/Vite-5-B73C9D?logo=vite&logoColor=white" alt="Vite"/>
  <img src="https://img.shields.io/badge/Material%20UI-5-0081CB?logo=mui&logoColor=white" alt="MUI"/>
  <img src="https://img.shields.io/badge/Redux%20Toolkit-2-593D88?logo=redux&logoColor=white" alt="Redux"/>
  <img src="https://img.shields.io/badge/Node.js-18+-339933?logo=node.js&logoColor=white" alt="Node.js"/>
  <img src="https://img.shields.io/badge/Express-4-000000?logo=express&logoColor=white" alt="Express"/>
  <img src="https://img.shields.io/badge/MongoDB-8-47A248?logo=mongodb&logoColor=white" alt="MongoDB"/>
  <img src="https://img.shields.io/badge/Redis-7-DC382D?logo=redis&logoColor=white" alt="Redis"/>
  <img src="https://img.shields.io/badge/Socket.IO-4-010101?logo=socket.io&logoColor=white" alt="Socket.IO"/>
  <img src="https://img.shields.io/badge/Docker-Compose-2496ED?logo=docker&logoColor=white" alt="Docker"/>
</p>

---

## 📖 Overview

**NMN Cinema** is a full-stack cinema management and online ticket booking platform built as a graduation thesis project. The system supports **3 distinct roles**:

- 🎥 **Customer:** Browse now-showing / upcoming movies, select showtimes, choose seats in real time, add food & drink combos, pay online via VNPay, receive QR Code e-tickets, rate & review movies, earn membership points, and interact with the AI chatbot.
- 🛡️ **Admin:** Full management dashboard — movies, showtimes, screening rooms, seats, combos, promotions, vouchers, banners, articles, users, roles & permissions, audit logs, and revenue analytics.
- 📱 **Staff:** Scan QR codes to verify tickets at the cinema entrance.

---

## 🏗️ Architecture

```
[ React + Vite (MUI, Redux) ]
        ↕ REST API (Axios)         ↕ WebSocket (Socket.IO)
[ Node.js + Express REST API ]  ←→  [ Socket.IO Server ]
        ↕                                  ↕
   [ MongoDB (Mongoose) ]        [ Redis (ioredis) ]
        ↕
[ VNPay ]  [ Nodemailer ]  [ Google OAuth ]  [ Gemini AI ]
```

- **Frontend** calls the backend via Axios REST API and Socket.IO for real-time seat locking
- **Redis** handles caching and distributed rate limiting
- **Node-cron** runs scheduled jobs (e.g., auto-expire held seats, showtime status updates)
- **Swagger UI** provides interactive API documentation at `/api-docs`
- **Docker Compose** starts MongoDB + Redis + API together

---

## 🛠️ Tech Stack

### Frontend
| Library / Tool | Version | Purpose |
|---|---|---|
| React | 18 | UI framework |
| Vite | 5 | Build tool & dev server |
| Material UI (MUI) | 5 | Component & icon library |
| MUI X Charts | 8 | Revenue & analytics charts (Admin) |
| Redux Toolkit | 2 | Global state management |
| React Router | 6 | Client-side routing |
| Socket.IO Client | 4 | Real-time seat locking |
| React Hook Form | 7 | Form validation |
| Axios | 1 | HTTP client |
| Swiper | 12 | Movie carousel slider |
| React Slick | 0.30 | Additional carousel support |
| QRCode / qrcode.react | 1 / 4 | QR Code generation & display |
| html5-qrcode | 2 | QR Code scanning (Staff) |
| DOMPurify | 3 | HTML sanitization |
| Moment.js | 2 | Date/time formatting |
| React Toastify | 10 | Toast notifications |

### Backend
| Library / Tool | Version | Purpose |
|---|---|---|
| Node.js | ≥ 18 | Runtime |
| Express | 4 | Web framework |
| Mongoose | 8 | MongoDB ODM (31 models) |
| Socket.IO | 4 | Real-time WebSocket server |
| ioredis | 5 | Redis client (caching, rate limiting) |
| JWT (jsonwebtoken) | 9 | Access & refresh token auth |
| Bcrypt | 5 | Password hashing |
| Zod | 3 | Request schema validation |
| Joi (via Zod) | — | Additional validation layer |
| Nodemailer | 6 | Transactional email (booking confirmation, reset password) |
| Multer | 2 | Image / file uploads |
| QRCode | 1 | QR Code generation for tickets |
| @google/generative-ai | 0.24 | Gemini AI chatbot integration |
| google-auth-library | 10 | Google OAuth 2.0 |
| Node-cron | 4 | Scheduled background jobs |
| Winston | 3 | Structured logging with correlation IDs |
| Morgan | 1 | HTTP request logging |
| Swagger (jsdoc + ui-express) | 6 / 5 | Interactive API documentation |
| Helmet | 7 | HTTP security headers |
| express-rate-limit | 7 | API rate limiting |
| express-mongo-sanitize | 2 | NoSQL injection prevention |
| xss-clean | 0.1 | XSS protection |
| hpp | 0.2 | HTTP parameter pollution prevention |
| Jest + Supertest | 29 / 6 | Unit & integration testing |

### DevOps & Infra
| Tool | Purpose |
|---|---|
| Docker & Docker Compose | Containerized deployment (MongoDB + Redis + API) |
| Winston Logger | Structured logging with correlation ID tracing |
| Node-cron | Scheduled jobs (seat expiry, showtime status sync) |

---

## ✨ Key Features

### 🎟️ Ticket Booking Flow
- Browse now-showing and upcoming movies
- Select showtime, screening room, and seat type
- **Real-time seat locking** via Socket.IO (prevents double booking)
- Add food & drink combos
- Apply vouchers / promotional codes
- Online payment via **VNPay**
- Receive **QR Code e-ticket** via email and on-screen

### 🔐 Authentication & Security
- Register / Login with email & password (JWT access + refresh tokens, HTTP-only cookies)
- **Google OAuth 2.0** login
- Forgot / Reset password via email link
- Role-based access control: Admin / Staff / Customer
- Redis-backed distributed rate limiting
- Helmet, CORS, NoSQL injection & XSS protection

### 🛡️ Admin Dashboard
- Revenue charts and analytics (MUI X Charts)
- Manage movies (with cast, genre, trailer, poster)
- Manage showtimes, screening rooms & seats
- Manage food/drink combos
- Manage promotions, vouchers, banners, and blog articles
- User management & role/permission assignment
- Audit log for admin actions

### 📱 Staff Panel
- Scan QR codes to verify ticket validity at the entrance (html5-qrcode)

### 🤖 AI Chatbot
- Movie recommendation chatbot powered by **Google Gemini AI**
- Maintains conversation history per session

### ⭐ Customer Features
- Movie ratings & reviews (with report/moderation system)
- Membership points system
- View booking history & download tickets
- Profile & account settings

### 📧 Email Notifications
- Booking confirmation with QR Code ticket
- Password reset link
- Membership welcome email

---

## 📁 Project Structure

```
DATN-Cinema/
├── backend/                           # REST API Server – Node.js + Express
│   ├── src/
│   │   ├── config/                    # MongoDB, Redis, Swagger, constants
│   │   ├── controllers/               # Request handler functions
│   │   ├── jobs/                      # Node-cron scheduled tasks
│   │   ├── middlewares/               # Auth, rate limiting, logging, error handling
│   │   ├── migrations/                # Database migration scripts
│   │   ├── models/                    # Mongoose schemas (31 models)
│   │   │   # Article, AuditLog, Banner, ChatMessage, ChatSession,
│   │   │   # Cinema, Combo, FAQ, FeaturedArticle, Feedback, Genre,
│   │   │   # MembershipInfo, Movie, MovieCategory, Order, Payment,
│   │   │   # Person, Promotion, PromotionRedeem, RefreshToken, Review,
│   │   │   # ReviewReport, Role, Room, SeatHold, Showtime, Ticket,
│   │   │   # TicketPricing, User, UserVoucher, Voucher
│   │   ├── routes/V1/                 # REST API routes (/api/v1/*)
│   │   ├── seeds/                     # Database seed scripts
│   │   ├── services/                  # Business logic layer (incl. redisService)
│   │   ├── test/                      # Unit & integration tests (Jest)
│   │   ├── utils/                     # AppError, helpers, Winston logger
│   │   ├── validations/               # Zod request schemas
│   │   ├── app.js                     # Express app setup (middleware stack)
│   │   └── server.js                  # HTTP server + Socket.IO entry point
│   ├── public/uploads/                # Uploaded images (served statically)
│   ├── .env.example                   # Environment variable template
│   ├── docker-compose.yml             # MongoDB + Redis services
│   ├── jest.config.js                 # Jest test configuration
│   └── Dockerfile
│
├── frontend/                          # React SPA – Vite + MUI
│   ├── src/
│   │   ├── apis/                      # Axios instance & API call functions
│   │   ├── components/                # Reusable UI components
│   │   ├── constants/                 # App-wide constants
│   │   ├── contexts/                  # React Context providers
│   │   ├── hooks/                     # Custom React hooks
│   │   ├── mocks/                     # Mock data for development
│   │   ├── pages/
│   │   │   ├── Admin/                 # Admin dashboard pages
│   │   │   ├── Auth/                  # Login, Register, Reset Password
│   │   │   ├── Client/                # Customer-facing pages
│   │   │   └── Staff/                 # Staff QR scanner page
│   │   ├── redux/                     # Redux Toolkit slices & store
│   │   ├── routes/                    # Route configuration
│   │   ├── services/                  # Client-side service functions
│   │   ├── theme/                     # MUI theme configuration
│   │   ├── utils/                     # Helper utilities
│   │   ├── App.jsx                    # Root component & routing
│   │   └── main.jsx                   # React entry point
│   └── vite.config.js
│
├── docs/                              # Project documentation
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

- [Docker & Docker Compose](https://docs.docker.com/get-docker/) — for containerized setup *(recommended)*
- Node.js ≥ 18 — for local development without Docker

### Option 1: Run with Docker (Recommended)

```bash
# 1. Clone the repository
git clone https://github.com/NguyenManhNinh/NMN-CENIMA.git
cd NMN-CENIMA

# 2. Configure backend environment
cd backend
cp .env.example .env
# Edit .env → set MongoDB URI, Redis URI, JWT secret, VNPay keys,
#              SMTP credentials, Google OAuth, Gemini API key

# 3. Start MongoDB + Redis + API
docker-compose up -d

# 4. Run frontend
cd ../frontend
npm install
npm run dev
```

| Service | URL |
|---|---|
| Frontend | `http://localhost:5173` |
| Backend API | `http://localhost:5000` |
| Swagger Docs | `http://localhost:5000/api-docs` |

### Option 2: Run Locally (Without Docker)

**Backend:**
```bash
cd backend
npm install
cp .env.example .env   # Edit all required values
npm run dev            # Starts at http://localhost:5000
```

**Frontend:**
```bash
cd frontend
npm install
npm run dev            # Starts at http://localhost:5173
```
---

## 👨‍💻 Author

**Nguyen Manh Ninh** 
