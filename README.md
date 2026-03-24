<div align="center">
  <h1>Blog Weave</h1>
  <p>Simple microservices-style demo (Posts + Comments) with a Vite/React client.</p>

  <p>
    <img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-5.9-blue" />
    <img alt="React" src="https://img.shields.io/badge/React-19-61dafb" />
    <img alt="Vite" src="https://img.shields.io/badge/Vite-8-646cff" />
    <img alt="Express" src="https://img.shields.io/badge/Express-5-black" />
  </p>
</div>

A simple microservices-style demo with:

- `posts/` — Posts service (Express)
- `comments/` — Comments service (Express)
- `client/` — React + Vite UI

Each backend service stores data **in memory** (restarts clear data).

## Prerequisites

- Node.js (this repo works well with modern Node versions; the services run `index.ts` directly)
- Package manager:
  - `pnpm` for `posts/` and `comments/` (a `pnpm-lock.yaml` is present)
  - `npm` (or `pnpm`) for `client/`

## Project structure

```
blog-weave/
  client/       # React + Vite frontend
  posts/        # Posts microservice
  comments/     # Comments microservice
```

## Services

### Posts service (`posts/`)

- Base URL: `http://localhost:4000`
- Endpoints:
  - `GET /posts` — returns all posts (object keyed by post id)
  - `POST /posts` — creates a post

Example:

```bash
curl -X POST http://localhost:4000/posts \
  -H "Content-Type: application/json" \
  -d '{"title":"Hello"}'

curl http://localhost:4000/posts
```

### Comments service (`comments/`)

- Base URL: `http://localhost:4001`
- Endpoints:
  - `GET /posts/:id/comments` — returns comments for a post
  - `POST /posts/:id/comments` — creates a comment for a post

Example:

```bash
curl -X POST http://localhost:4001/posts/<POST_ID>/comments \
  -H "Content-Type: application/json" \
  -d '{"content":"Nice post"}'

curl http://localhost:4001/posts/<POST_ID>/comments
```

## Run locally

> You’ll want **3 terminals**: one per service + one for the client.

### 1) Start `posts`

```bash
cd posts
pnpm install
pnpm start
```

Runs on `http://localhost:4000`.

### 2) Start `comments`

```bash
cd comments
pnpm install
pnpm start
```

Runs on `http://localhost:4001`.

### 3) Start the `client`

```bash
cd client
npm install
npm run dev
```

Vite runs on `http://localhost:5173`.

## Notes

- Data is stored in memory (restarting services resets posts/comments).
- The frontend is currently the default Vite/React template; you can extend it to call the services on ports `4000` and `4001`.
