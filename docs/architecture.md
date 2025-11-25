# Awakeningspirit.ist – Web Architecture

> Super simple, clean, minimalist info site for now. Designed to evolve over time into a richer church site with sermons, events, and optional WordPress/headless integration.

---

## 1. Goals

- **Clear & calm experience** for visitors looking for:
  - Service times
  - Location & contact
  - Basic info about beliefs, leadership, and ministries
- **Minimal but modern** UI: clean typography, generous whitespace, subtle motion if any.
- **SEO-friendly** and fast.
- **Easy to evolve**:
  - Start with file-based content (JSON/MD).
  - Later integrate with a headless CMS (e.g. WP, Sanity, etc.) without rewriting UI.
- **Octohost-friendly**:
  - Containerized
  - Port **4000**
  - Attached to the `proxy` network
  - Health endpoint at `/health` returning `{ ok: true }`
  - Contact endpoint at `/api/contact` using SendGrid via `SMTP_PASS_FILE`

---

## 2. Tech Stack

### 2.1 Frontend

- **Framework:** Next.js (React + TypeScript), App Router
- **Language:** TypeScript
- **Styling:**
  - Tailwind CSS
  - Small layer of custom layout and UI primitives (Section, Card, Button, etc.)
- **Forms & validation (planned):**
  - `react-hook-form`
  - `zod` for schema-based validation
- **State/data:**
  - Mostly component-local state and server components
  - TanStack Query (React Query) if/when we need client-side data fetching

### 2.2 Backend / API

- Next.js **route handlers** under `app/api/*` for:
  - `/api/health` or `/health`
  - `/api/contact`
- Future: an internal content layer that can talk to:
  - File-based content in the repo (Phase 1)
  - WordPress or another headless CMS (Phase 2)

---

## 3. Runtime Contracts

These contracts are important for deployment + monitoring, especially on Octohost.

### 3.1 Health Check

- **Route:** `GET /health`
- **Response:** `200 OK` and JSON:

```json
{
  "ok": true
}
