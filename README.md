# Tee Shop — storefront + admin panel

Next.js 14 (App Router) · TypeScript · PostgreSQL · Prisma · Auth.js (NextAuth) · zod

## Run it locally
1. `cp .env.example .env` and fill in `DATABASE_URL` and `NEXTAUTH_SECRET`
2. `npm install`
3. `npm run db:push` — creates the tables
4. `npm run db:seed` — creates your Owner login + one sample product
5. `npm run dev` → store at http://localhost:3000, admin at http://localhost:3000/admin

## Roles (edit in `src/lib/permissions.ts`)
| Role    | Products | Orders | Storefront text | Staff accounts |
|---------|:-:|:-:|:-:|:-:|
| Owner   | ✓ | ✓ | ✓ | ✓ |
| Manager | ✓ | ✓ | ✓ |   |
| Editor  |   |   | ✓ |   |
| Support |   | ✓ |   |   |

## Before going live
- Change the seeded Owner password; use a long random `NEXTAUTH_SECRET`
- Replace disk uploads in `src/app/api/upload/route.ts` with Cloudinary / S3 / Vercel Blob
- Plug a payment gateway into `src/app/cart/page.tsx` (marked PAYMENT HOOK) and mark orders PAID from its webhook
- Add order-confirmation emails (Resend / Postmark) inside `src/app/api/orders/route.ts`
- Add login rate-limiting (e.g. Upstash Ratelimit) and HTTPS (automatic on Vercel)
