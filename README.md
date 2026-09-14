# Bandobast

Bandobast is a SaaS for event vendors and photographers in India. It manages bookings, finances, services, team, and photo delivery in one place. It replaces the Excel sheets, WhatsApp threads, and Google Drive links vendors currently juggle.

Live at [bandobast.in](https://bandobast.in). Built by [Pranay Ghuge](https://github.com/Pranay0205). The production repository is private. This repo is a public showcase of the product and the architecture behind it.

## Traction

- Active paying customers: [YOUR INPUT: number of active paying customers]
- Bookings managed so far: [YOUR INPUT: total bookings managed to date]
- Client photos delivered: [YOUR INPUT: total photos delivered to clients]
- Monthly recurring revenue: [YOUR INPUT: monthly recurring revenue]
- Launched: [YOUR INPUT: month and year the first customer went live]

## The problem

Small event vendors, photographers, venues, and planners run their business on Excel and WhatsApp. Bookings get double-booked. Post-event photo deliveries slip past deadlines. Client photos go out over ad-hoc Drive links with no privacy control.

## What it does

- **Bookings.** Per-employee availability with overlapping date and time range detection, so a vendor never double-books. A booking, its blocked slots, and its delivery tasks are created inside one database transaction.
- **Task boards.** Booking time auto-creates kanban delivery tasks, and a background worker marks overdue work, so missed post-event deadlines surface on their own.
- **Services.** Per-category JSON schemas drive service fields, so photography and venues share one code path instead of separate ones.
- **Team.** Five role types with employee-level role-based access control.
- **Photos.** Privacy-focused pipeline managing around 10K photos per customer. libvips generates three thumbnail sizes plus compressed previews, uploads them to Cloudflare R2, verifies storage, then deletes the original upload.
- **Finance.** Subscription checks run in the request pipeline. Vendor interviews validated a Rs. 499/month price point.

## Architecture

The full system overview lives in [ARCHITECTURE.md](ARCHITECTURE.md). Short version: a Go and Echo monolith with Handler to Service to Repository layers, a Next.js SSR frontend sitting in front of the internal API, tenant isolation at the application and database layers, and five Docker Compose services on a single VPS.

## Tech stack

Go, Echo, Next.js, React, TypeScript, PostgreSQL 16, sqlc, goose, libvips, Cloudflare R2, Docker Compose, Hetzner, Cloudflare Tunnel.

## Screenshots

[YOUR INPUT: screenshot of the booking calendar showing employee availability, saved as screenshots/booking-calendar.png]
![Booking calendar](screenshots/booking-calendar.png)

[YOUR INPUT: screenshot of the kanban delivery task board, saved as screenshots/task-board.png]
![Task board](screenshots/task-board.png)

[YOUR INPUT: screenshot of the client photo delivery gallery, saved as screenshots/photo-delivery.png]
![Photo delivery](screenshots/photo-delivery.png)

## Discovery

Interviewed small Indian wedding vendors before building. Focused the MVP on workflows they already ran through Excel and WhatsApp. Planned a 26-week path to soft launch, prioritizing auth, service setup, bookings, public widgets, and task boards before add-on monetization features.

## Contact

- GitHub: [github.com/Pranay0205](https://github.com/Pranay0205)
- Site: [pranayghuge.com](https://pranayghuge.com)
