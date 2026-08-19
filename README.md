<div align="center">

# Fuyad Hasan Fahim

**Full-stack engineer building business systems, billing workflows and reliable backends.**

[![Website](https://img.shields.io/badge/Website-22D3EE?style=flat-square&logo=vercel&logoColor=0B0B0F)](https://fuyadhasanfahim.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-3B82F6?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/codewithfuyad)
[![X](https://img.shields.io/badge/X-6366F1?style=flat-square&logo=x&logoColor=white)](https://x.com/codewithfuyad)
[![Email](https://img.shields.io/badge/Email-8B5CF6?style=flat-square&logo=gmail&logoColor=white)](mailto:codewithfuyad@gmail.com)

</div>

---

I build the software companies run their operations on — ERP and HR platforms, client delivery portals, billing flows, and the document, notification and real-time layers underneath them. Most of my work is backend-leaning: schema design, service boundaries, payment correctness, and background processing, wrapped in interfaces non-technical staff use daily.

The problems I care about are the unglamorous ones: what happens when a webhook arrives twice, when a payroll run is approved with the wrong total, when a transaction fails halfway.

---

## Selected Engineering Work

### Webbriks ERP & HR Platform

> A four-application monorepo — separate auth, dashboard and support front-ends over a single Express + TypeScript API — covering payroll, attendance, leave, quotations, invoicing, CRM leads and customer support.

This is my deepest backend work. Order and quotation writes run inside **MongoDB transactions**, so the Docker Compose stack provisions Mongo as a single-node replica set rather than a plain instance. Cross-service side effects go through a **transactional outbox** with a claim/dispatch/retry worker instead of firing inline. Payroll runs are guarded by a lock document and an amount-mismatch check that completes **before any transaction opens**, so an unconfirmed out-of-tolerance run performs zero writes.

Also present: append-only audit logging, BullMQ/Redis queues, Sentry and structured `pino` logging, `/healthz` with graceful shutdown, boot-time environment validation, Socket.io namespaces behind an auth middleware, and Puppeteer-rendered quotation and receipt PDFs. A GitHub Actions workflow gates the server on `tsc --noEmit`.

`TypeScript` `Next.js` `Express` `MongoDB` `Redis / BullMQ` `Socket.io` `Better Auth` `Sentry` `Docker` `GitHub Actions`

**[Repository →](https://github.com/fuyadhasanfahim/dev-hr-management)**

---

### Ledger — a Stripe integration you can break on purpose

> Subscriptions, one-time checkout, marketplace splits, refunds and failed-payment recovery, with the webhook layer exposed in a live event log.

Most payment demos show the happy path. Ledger lets you trigger the failure modes yourself, then inspect what the system actually did.

Idempotency is enforced by a **unique database index, not an `if` statement** — the event ID is inserted first, so a concurrent replay loses the race inside MongoDB and surfaces as a duplicate-key error. Handlers that *failed* stay retryable; handlers that succeeded never re-run. The rule enforced throughout: returning from checkout with `?status=success` grants nothing — only a signature-verified webhook moves money-derived state.

`Next.js 16` `React 19` `TypeScript` `Stripe` `MongoDB`

**[Repository →](https://github.com/fuyadhasanfahim/ledger)** · **[Live demo →](https://ledger-alpha-green.vercel.app)** (Stripe test mode)

---

### An-Nisa — commerce platform and admin back office

> A storefront with a full admin panel, built on PostgreSQL and Prisma.

Ten **sequential migrations** carry the schema: inventory, SKUs, discount pricing, shipping and payment totals, customer public IDs and expense tracking were each introduced as deliberate changes rather than one retrofitted model. Role-based access via Better Auth, server-rendered PDF invoices, and three Gemini-backed endpoints for product description generation, content checking and chat.

`Next.js` `TypeScript` `PostgreSQL` `Prisma` `Better Auth` `Google Gemini`

**[Repository →](https://github.com/fuyadhasanfahim/an-nisa)** · **[Live demo →](https://an-nisa.vercel.app)**

---

### Client Delivery Portal

> The full commercial lifecycle for a service business: quote request, order, revision rounds, invoicing and file delivery.

Payments run through **both Stripe and PayPal** behind one order flow. Large design assets bypass the API entirely using **S3 presigned URLs**, so uploads never pass through application memory. Order conversations and notifications are delivered over Socket.io, and each lifecycle transition triggers its own transactional email template. Built across roughly 380 commits.

`Next.js` `Express` `TypeScript` `MongoDB` `Stripe` `PayPal` `AWS S3` `Socket.io` `Redux Toolkit`

**[Client →](https://github.com/fuyadhasanfahim/client-portal-client)** · **[Server →](https://github.com/fuyadhasanfahim/client-portal-server)**

---

## Tooling & Automation

| Project | What it does |
|---|---|
| **[backup-core](https://github.com/fuyadhasanfahim/backup-core)** | Scheduled MongoDB backup service — cron-driven dumps, `tar.gz` compression, rclone off-site sync, retention cleanup and email alerts on failure, behind a Next.js monitoring dashboard. Containerized. |
| **[image-downloader](https://github.com/fuyadhasanfahim/image-downloader)** | Node CLI for bulk image pipelines — parses Excel sheets with auto-detected headers, downloads with bounded concurrency, and resumes after interruption. |

---

## Core Stack

| | |
|---|---|
| **Languages** | TypeScript (primary), JavaScript |
| **Frontend** | Next.js (App Router), React, Tailwind CSS, shadcn/ui, Redux Toolkit, TanStack Query |
| **Backend** | Node.js, Express, Socket.io, Zod, BullMQ, Puppeteer |
| **Databases** | MongoDB / Mongoose, PostgreSQL / Prisma, Redis |
| **Auth** | Better Auth, JWT, role-based authorization |
| **Payments** | Stripe (Checkout, Connect, webhooks), PayPal |
| **Infrastructure** | Docker, GitHub Actions, AWS S3, Cloudinary, Sentry, pino |

---

## Engineering Principles

- **Let the database enforce integrity.** Unique constraints and transactions settle races that application-level checks lose under concurrency.
- **Explicit boundaries between layers.** Routes stay thin, services hold the logic, validators sit at the edge — the same shape across every backend I maintain.
- **Design for failure.** Retryable workers, graceful shutdown, boot-time config validation, and documented limitations instead of silent ones.

## Engineering Focus

Deepening the operational side of what I already ship — queue-backed background work, observability, and containerized environments that match production behaviour. Extending CI coverage outward from the calculation-heavy code where tests pay off most.

---

## Contact

Available for freelance projects, remote full-time roles, and technical collaboration. If you're working on internal tooling, a billing system, or a platform that has outgrown its first architecture — that's the work I do best.

**[fuyadhasanfahim.com](https://fuyadhasanfahim.com)** · **[LinkedIn](https://www.linkedin.com/in/codewithfuyad)** · **[X](https://x.com/codewithfuyad)** · **[codewithfuyad@gmail.com](mailto:codewithfuyad@gmail.com)**
