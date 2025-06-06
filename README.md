# EaseChat – Embeddable AI Chat Widget with Analytics

An AI-powered chat widget you can drop into any website, plus a modern dashboard to track user conversations and analytics.



## Table of Contents

1. [Features](#features)
2. [Architecture](#architecture)
3. [Tech Stack](#tech-stack)
4. [Getting Started](#getting-started)
   1. [Prerequisites](#prerequisites)
   2. [Install & Dev](#install--dev)
   3. [Environment Variables](#environment-variables)
5. [Project Structure](#project-structure)
6. [Embedding the Widget](#embedding-the-widget)
7. [Deployment & Demos](#deployment--demos)
8. [Challenges & Solutions](#challenges--solutions)
9. [Contributing](#contributing)
10. [License](#license)

---

## Features

- **Embeddable Widget:** AI chat powered by WebSocket + Express API
- **Multi-user Support:** Each user can mint multiple widgets
- **Analytics Dashboard:** Conversation metrics, usage trends, and more
- **Zero-Config Embed:** Copy & paste a single `<script>` tag
- **Real-time Updates:** Socket.io for live chat sessions

## Architecture

**Monorepo** with [Turborepo](https://turborepo.org/) & Bun:

- **apps/chat-widget** – React + Vite embeddable widget
- **apps/web** – Next.js dashboard & HTTP API
- **apps/backend** – Bun + Express + Socket.io server
- **packages/db** – Prisma client & database layer

### Data Flow

1. Widget opens a WebSocket to `backend` → streams user messages.
2. Backend invokes AI via `gemini API` → pushes responses back.
3. REST calls from `web` (Next.js) read/write analytics via `packages/db`.
4. Dashboard UI shows aggregated metrics and real-time sessions.

## Tech Stack

- **Language**: TypeScript
- **Frameworks**: React, Next.js, Express, Socket.io
- **Bundler**: Vite (widget), Turbo (monorepo)
- **Runtime**: Node.js ≥18 & [Bun](https://bun.sh/)
- **DB**: Prisma + PostgreSQL database
- **Deployment**: Digital Ocean (socketio server and nextjs server), GitHub Pages (widget via `gh-pages`)

## Getting Started

### Prerequisites

- Node.js ≥18
- [Bun](https://bun.sh/) v1.2.9+ (for backend & db)
- (Optional) Yarn, npm or pnpm

### Install & Dev

Clone & install:

```bash
git clone https://github.com/aadithya2112/EaseChat
cd EaseChat
# install everything
bun install
```

Run all services in dev mode:

```bash
bun run dev
# → dashboard & widget & backend start concurrently
```

Individually: (Recommended)

- **Generate Prisma Client**
  ```bash
  cd packages/db && bunx prisma generate
  ```
- **Dashboard (Next.js)**
  ```bash
  cd apps/web && bun run dev
  ```
- **Widget (Vite)**
  ```bash
  cd apps/chat-widget && bun run dev
  ```
- **Backend (Socket.io)**
  ```bash
  cd apps/backend && bun src/index.ts
  ```

### Environment Variables

Create a `.env` (for each app) from `.env.example`:

```env
# apps/backend/.env
GOOGLE_GENAI_API_KEY="…"

# apps/web/.env
DATABASE_URL="postgres://user:pass@localhost:5432/db"
JWT_SECRET="…"

# packages/db/.env
DATABASE_URL="postgres://user:pass@localhost:5432/db" # Same as web
```

```

## Project Structure

```

/
├─ apps/
│ ├─ chat-widget/ # React widget (Vite)
│ ├─ web/ # Dashboard & HTTP API (Next.js)
│ └─ backend/ # WebSocket server (Bun + Express)
└─ packages/
├─ db/ # Prisma client & migrations

````



