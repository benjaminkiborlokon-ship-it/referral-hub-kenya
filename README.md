# Referral Hub Kenya

Mobile-first referral discovery, paid referral-link promotion, manual M-Pesa verification, advertising click credits, and a private admin dashboard.

## Stack
- Next.js 14 / React 18 / TypeScript
- PostgreSQL + Prisma
- Secure signed admin session cookie
- Server-side validation with URL/phone checks
- Backend ad click accounting with database-side remaining-click decrement
- PWA manifest

## Production setup
1. Create a PostgreSQL database and set `DATABASE_URL`.
2. Set a long random `SESSION_SECRET` (at least 32 characters).
3. Set `ADMIN_EMAIL` and a strong `ADMIN_PASSWORD` for the initial seed.
4. Run `npm install`.
5. Run `npx prisma migrate deploy` (or `npm run db:push` for a new database).
6. Run `npm run db:seed`.
7. Run `npm run build && npm start`.

## Environment
See `.env.example`.

## Manual M-Pesa verification
Applicants may submit a transaction code or full SMS. The server stores the original message and extracts possible fields, but **SMS text is never treated as proof of payment**. An administrator must verify the transaction against the actual M-Pesa record before approval.

## Payment/listing isolation
Each referral application stores its own purchased price and duration. A unique transaction-code constraint spans referral and ad applications at the application layer, preventing the same code from being submitted to both workflows.

## Advertising
Advertisers buy click credits. Only approved ads become active. Each valid click is counted server-side; a database conditional decrement prevents the remaining balance from going below zero. A one-hour IP/session cooldown reduces rapid duplicate clicks.

## Important before public launch
- Replace seed credentials immediately.
- Use a managed PostgreSQL provider and HTTPS.
- Add a real M-Pesa/Daraja integration if automated verification is later desired.
- Add a proper object-storage upload flow for logos/banner images rather than trusting arbitrary remote image URLs.
- Add privacy policy, terms, advertising/referral disclosures, and a clear abuse/contact process.
