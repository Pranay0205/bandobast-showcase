# Bandobast

SaaS for event vendors and photographers in India. Up and running with active customers.

If I put it shortly, it is their website plus booking system plus photo delivery in one place.

Live at [bandobast.in](https://bandobast.in)

## The problem

Event vendors and photographers in India run their business on WhatsApp and spreadsheets. Client photos get shared over Google Drive links that expire, get lost, or look unprofessional. Bookings are tracked in notebooks. There is no single place where a vendor's online presence, bookings, and client delivery live together.

## What it does

**Vendor website.** Every vendor gets a professional online presence to showcase their work and attract clients.

**Booking system.** Clients can book vendors through the platform. Vendors manage their bookings, availability, and client communication in one dashboard.

**Photo delivery.** Photographers deliver finished galleries directly to clients through the platform. No more Drive links. Clients get a clean, branded gallery experience.

## Who uses it

Event vendors and photographers across India, serving real clients for weddings and events.

> TODO for Pranay: add real numbers here. How many vendors are on the platform? How many bookings or galleries delivered so far? One honest paragraph of traction beats everything else on this page.

## Screenshots

> TODO for Pranay: drop screenshots here. Suggested shots:
> - Vendor public website / portfolio page
> - Booking dashboard
> - Client photo gallery view
> - Mobile views if they look good

## Architecture

The platform is built as a multi-tenant SaaS. Each vendor gets their own storefront, booking pipeline, and media delivery space, all managed from a single dashboard.

> TODO for Pranay: confirm the stack and I will write this up properly. Suggested outline:
> - Frontend framework and hosting
> - Backend language and framework
> - Database
> - How photo storage and delivery works (S3? CDN?)
> - How multi-tenancy is handled

## Why I built it

I wanted to build something real people pay for and use every day, not another tutorial project. Bandobast is a complete product: marketing site, authenticated dashboards, payments-adjacent booking flows, and large media file handling. It is the project that taught me the most about building for real users.

## Contact

Pranay Ghuge
- pranayghuge02@gmail.com
- [github.com/Pranay0205](https://github.com/Pranay0205)
- [linkedin.com/in/pranay-ghuge-2a4a75137](https://linkedin.com/in/pranay-ghuge-2a4a75137)
