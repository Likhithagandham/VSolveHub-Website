# VSolveHub Website

Customer-facing service booking platform for **V Solve Hub** — discover services, verify via OTP, book instantly, and track status.

> App code lives in [`VSolveHub/`](./VSolveHub).

## Features

- **Homepage** — search, quick services, promos, popular & saved services
- **Services catalog** — browse by category or search by name/tag
- **Service detail** — pricing, duration, tags, book now
- **OTP auth** — mock OTP `1234`, cookie-based sessions
- **Booking** — time slot + address, Zod validation
- **Tracking** — simulated status progression (`SEARCHING` → `COMPLETED`)
- **Profile** — bookings, saved services, addresses

## Tech stack

| Layer | Choice |
|-------|--------|
| Framework | Next.js 15 (App Router) |
| UI | React 19, TypeScript, Vanilla CSS |
| Database | SQLite + Prisma ORM |
| Validation | Zod |

## Getting started

```bash
cd VSolveHub
npm install
```

Create `.env` in `VSolveHub/`:

```env
DATABASE_URL="file:./dev.db"
```

Set up the database and seed demo data:

```bash
npm run db:push
npm run db:seed
```

Run the dev server:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

> If styles look broken, stop all `npm run dev` processes, delete `.next`, and restart.

## Demo credentials

| Field | Value |
|-------|-------|
| Phone | `9876543210` |
| OTP | `1234` |
| Sample booking | `VSH-DEMO-001` |

## Project structure

```
VSolveHub/
├── app/
│   ├── (customer)/          # Pages: home, services, booking, profile
│   ├── api/                 # Auth, catalog, bookings, profile APIs
│   ├── globals.css          # Design system
│   └── layout.tsx
├── components/
│   ├── customer/            # Home, booking, profile UI
│   ├── shared/              # AppShell (header + bottom nav)
│   └── ui/                  # Buttons, inputs, SVG service icons
├── lib/
│   ├── auth/                # Session + mock OTP
│   ├── bookings/            # Booking queries + status simulation
│   ├── catalog/             # Prisma catalog + display data
│   └── validation/          # Zod schemas
└── prisma/
    ├── schema.prisma
    └── seed.ts
```

## API routes

| Route | Purpose |
|-------|---------|
| `POST /api/auth/otp` | Send / verify OTP |
| `GET /api/auth/session` | Current user session |
| `GET /api/catalog` | Categories & services |
| `GET /api/catalog/search` | Search services |
| `POST /api/bookings` | Create booking |
| `GET /api/bookings/[ref]` | Booking details |
| `GET /api/bookings/[ref]/status` | Live status |
| `GET/POST /api/profile/addresses` | Manage addresses |
| `GET/POST /api/profile/saved` | Saved services |

## Scripts

```bash
npm run dev          # Start dev server
npm run build        # Production build
npm run start        # Start production server
npm run db:generate  # Generate Prisma client
npm run db:push      # Sync schema to SQLite
npm run db:seed      # Seed demo data
```

## Seeded services

| Service | Category | Price |
|---------|----------|-------|
| Plumbing | Home Repair | ₹299 |
| Electrician | Home Repair | ₹349 |
| AC Repair | Home Repair | ₹499 |
| Deep Cleaning | Cleaning | ₹1,999 |
| Home Salon | Beauty | ₹999 |
| Washing Machine Repair | Appliance Repair | ₹399 |

## Roadmap

- [ ] Provider-side app & real dispatch
- [ ] SMS OTP integration
- [ ] Payment gateway
- [ ] Location picker & maps

## License

Private — V Solve Hub
