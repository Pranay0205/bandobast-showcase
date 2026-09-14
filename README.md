# Bandobast

Bandobast is a SaaS for event vendors and photographers in India. It manages bookings, finances, services, team, and photo delivery in one place, replacing the Excel sheets, WhatsApp threads, and Google Drive links vendors currently juggle.

Built by [Pranay Ghuge](https://github.com/Pranay0205). The production repository is private. This is a public showcase of the architecture and the product thinking behind it.

## The problem

Small event vendors, photographers, venues, planners, run their business on Excel and WhatsApp. Bookings get double-booked, post-event photo deliveries slip past deadlines, and client photos go out over ad-hoc Drive links with no privacy control.

## What it does

- **Bookings.** Per-employee availability with overlapping date and time range detection, so a vendor never double-books. A booking, its blocked slots, and its delivery tasks are created inside one database transaction.
- **Task boards.** Booking time auto-creates kanban delivery tasks, and a background worker marks overdue work, so missed post-event deadlines surface on their own.
- **Services.** Per-category JSON schemas drive service fields, so photography and venues share one code path instead of separate ones.
- **Team.** Five role types with employee-level role-based access control.
- **Photos.** Privacy-focused pipeline. libvips generates three thumbnail sizes plus compressed previews, uploads them to Cloudflare R2, verifies storage, then deletes the original upload.
- **Finance.** Subscription checks run in the request pipeline. Vendor interviews validated a Rs. 499/month price point.

## Architecture

- **Go/Echo monolith**, Handler to Service to Repository layers, with eight independently testable feature modules.
- **BFF-style**: Next.js SSR sits in front of the internal Go API. JWTs live in HTTP-only cookies, and authenticated JSON payloads never reach the browser.
- **Tenant isolation** at both the application and database layers. Repository queries are scoped with `tenant_id` and backed by PostgreSQL 16 Row-Level Security.
- **Request pipeline** is standardized around rate limiting, JWT validation, RBAC, tenant context, and subscription checks before any handler logic runs.
- **Type-safe database access** with sqlc and goose migrations embedded via `embed.FS`, across roughly 25 tables.
- **Lean infrastructure**: five Docker Compose services on a single Hetzner VPS, with Cloudflare Tunnel exposing only the frontend.

## Discovery

Interviewed small Indian wedding vendors before building. Focused the MVP on workflows they already ran through Excel and WhatsApp. Planned a 26-week path to soft launch, prioritizing auth, service setup, bookings, public widgets, and task boards before add-on monetization features.

## Tech stack

Go, Echo, Next.js, React, TypeScript, PostgreSQL 16, sqlc, goose, libvips, Cloudflare R2, Docker Compose, Hetzner, Cloudflare Tunnel.

## Screenshots

Coming soon.

## Contact

- GitHub: [github.com/Pranay0205](https://github.com/Pranay0205)
- Site: [pranayghuge.com](https://pranayghuge.com)
