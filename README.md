# ubinote (web)

Vite + React + TypeScript frontend for the ubinote API. Notes are stored and edited as Markdown, rendered with GitHub-flavored Markdown.

The app talks to a Go API (default `http://localhost:8080`). Authentication uses an HttpOnly `token` cookie; every request is sent with `credentials: 'include'`. A `401` clears the session and sends you back to login.

## Prerequisites

- Node.js 20+
- The ubinote API running and reachable at `VITE_API_URL`

## Setup

```bash
npm install
cp .env.example .env
npm run dev
```

Open http://localhost:5173.

## Environment

| Variable       | Default                 | Purpose                                |
|----------------|-------------------------|----------------------------------------|
| `VITE_API_URL` | `http://localhost:8080` | Base URL of the Go API (no trailing `/`) |

## Scripts

| Command           | What it does                          |
|-------------------|---------------------------------------|
| `npm run dev`     | Start the Vite dev server             |
| `npm run build`   | Typecheck and build to `dist/`        |
| `npm run preview` | Serve the production build            |
| `npm run lint`    | Run oxlint                            |

## Routes

| Path                 | Page                                      |
|----------------------|-------------------------------------------|
| `/login`             | Sign in                                   |
| `/register`          | Create an account, then sign in           |
| `/`                  | Notes list (signed in)                    |
| `/notes/new`         | Create a note                             |
| `/notes/:id`         | Read a note                               |
| `/notes/:id/edit`    | Edit a note with a live Markdown preview  |

Anything else redirects to `/`. List, view, create, and edit require a session.

## Features

- Register, login, and logout against `/api/v1/auth/*` and `/api/v1/me`
- List, create, update, and delete notes on `/api/v1/notes`
- Markdown editor toolbar (headings, emphasis, lists, tasks, quotes, code, links) and a side-by-side preview
- Light and dark theme, stored in `localStorage` under `ubinote_theme`, falling back to the system preference
