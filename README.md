# Referral Hub Kenya

Production-ready Next.js + PostgreSQL referral marketplace foundation with:
- Mobile-first public UI
- Admin authentication and private dashboard
- Unlimited referral offers/categories
- Referral-link promotion applications
- Manual M-Pesa verification workflow
- Unique transaction-code protection
- Separate pay-per-click advertising workflow
- Backend ad-click accounting with IP cooldown and server-side limits
- Configurable price, duration, M-Pesa number and instructions
- Deployment-ready Docker configuration

## Local setup
1. Copy `.env.example` to `.env` and set a strong `SESSION_SECRET`, database URL, admin email/password.
2. `npm install`
3. `npx prisma db push`
4. `npm run db:seed`
5. `npm run dev`

## Production
Use a managed PostgreSQL database, HTTPS, a strong random SESSION_SECRET, and change the seeded admin password before launch. Run `npm run build && npm start`.

### Important payment note
M-Pesa SMS text is treated as an untrusted claim. It is stored for audit and parsing only; an admin must verify the payment against the actual M-Pesa record before approval.
