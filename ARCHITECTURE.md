# Bandobast architecture

One-page overview of how the system fits together. For the product story, see [README.md](README.md).

## Shape of the system

A Go and Echo monolith organized in Handler to Service to Repository layers, with eight independently testable feature modules. A Next.js SSR frontend sits in front of the internal Go API, so authenticated JSON payloads never reach the browser. JWTs live in HTTP-only cookies.

## Booking flow

A vendor creates a booking for a date and time range. The service layer checks per-employee availability and rejects overlapping ranges, so nobody gets double-booked. The booking, its blocked time slots, and its delivery tasks are written inside one database transaction, so a partial failure never leaves the schedule half-written. Creating the booking also auto-creates kanban delivery tasks for the post-event work.

A background worker scans for overdue delivery tasks and flags them. [YOUR INPUT: what runs the background worker, e.g. a Go routine, a cron job, or a queue]

## Photo delivery flow

After the event, the vendor uploads the shoot. libvips generates three thumbnail sizes plus compressed previews. The pipeline uploads everything to Cloudflare R2, verifies the storage, then deletes the original upload. Around 10K photos per customer flow through this path. Clients get private gallery links instead of ad-hoc Drive shares.

## Data model

Roughly 25 tables in PostgreSQL 16, with type-safe access through sqlc and goose migrations embedded in the binary. Every tenant's data is scoped by tenant_id in the repository layer and enforced again by Row-Level Security in the database, so one vendor can never see another vendor's bookings.

## Request pipeline

Every request passes through the same pipeline before any handler logic runs: rate limiting, JWT validation, role-based access control, tenant context, and subscription checks.

## Deployment

Five Docker Compose services on a single Hetzner VPS. [YOUR INPUT: names of the five Docker Compose services] Cloudflare Tunnel exposes only the frontend, so the API and database never touch the public internet. [YOUR INPUT: how deploys work, manual steps or CI]
