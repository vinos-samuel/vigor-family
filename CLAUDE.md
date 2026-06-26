# Vigor Family — CLAUDE.md

## Project Overview
Vigor Family is a separate app from Vigor (solo). Same tech stack, separate Supabase project, separate GitHub repo.

**Repo:** https://github.com/vinos-samuel/vigor-family
**Stack:** React Native + Expo + TypeScript + NativeWind (mobile) / Hono + Supabase + Bun (backend)

## Current Sprint
Project scaffolded. No features built yet.
Next: Supabase project setup → mobile app init → backend init → family creation flow.

## Stack
- Mobile: React Native + Expo + TypeScript + NativeWind
- Backend: Hono + TypeScript + Bun
- DB + Auth: Supabase (separate project from solo Vigor)
- Payments: Stripe (family plan ~$9-12/month)
- Push notifications: Expo Notifications

## MVP Build Order
1. Supabase project setup (schema: users, families, members, check-ins, add-ons)
2. Mobile app init (Expo)
3. Backend init (Hono on Bun)
4. Auth (Supabase Auth)
5. Family creation + invite flow
6. Child vs adult profile types
7. Points system
8. Family dashboard + leaderboard
9. 8pm digest push notification with conversation prompt
10. Add-on library (pick up to 3)
11. 90-day collective goal tracker
12. Parent view of kids (on track/off track only)
13. Stripe family plan

## Key Design Decisions
- Separate Supabase project from solo Vigor (clean separation)
- Solo Vigor linked only via soft referral on Family profile page
- No per-seat pricing — one family plan up to 6 members
- Child profiles: no calorie numbers shown to parents, only on-track/off-track

## Deployment
- Mobile: Expo EAS → App Store (new app listing)
- Backend: TBD (match solo Vigor hosting once decided)
