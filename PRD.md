# Rally — Product Requirements Document

**Version:** 1.0  
**Date:** 2026-06-08  
**Status:** Approved for MVP build

---

## 1. Product Vision

**Rally** is a family health accountability app. Not a calorie tracker. A catalyst for families to talk about health together.

**Hero line:** *"There is appetite to bring health into conversation — but no avenue."*

**Category:** Family health accountability. No direct competitor owns this space.

**The moment Rally is built for:** Your child asks at dinner — *"Did you hit your water today? I got mine."*

---

## 2. Relationship to Vigor (Solo)

- Rally is a **separate app** — separate codebase, separate Supabase project, separate App Store listing
- Solo Vigor users are linked via a soft referral on the Rally profile page: *"Tracking solo too? Download Vigor →"*
- No data shared between apps

---

## 3. User Types

| Type | Age | Who manages account |
|------|-----|---------------------|
| Parent / Admin | Any | Themselves |
| Adult Member | Any | Themselves |
| Teen | 16+ | Themselves (parent assigns adult profile) |
| Child | Under 16 | Parent manages account |

### Parent / Admin
- Full personal tracking (calories, movement, hydration)
- Invites members, sets family name, sets family goal
- Picks family add-ons (up to 3 from library)
- Toggles accountability mode (post-MVP)
- Assigns child vs adult profile per member
- Manages child accounts directly — no separate child login

### Adult Member / Teen
- Full personal tracking: calories in, calories out, movement, hydration
- Sees own dashboard + family dashboard
- Own Supabase Auth login

### Child (under 16)
- No separate login — parent logs on their behalf or logs from parent's device
- No calorie counting — eating habits only
- Tracks: movement, hydration, "how well did I eat?" (3-tap: Mostly healthy / Mixed / Could be better)
- Optional: "Did I get up fresh?"
- Child sees their own data on a simplified view
- Parent sees: streak + on track / off track only — no raw numbers

---

## 4. Core Tracking

| Member type | Tracks |
|-------------|--------|
| Adult / Teen | Calories in, calories out, movement, hydration |
| Child | Movement, hydration, eating habit self-rating (3-tap) |
| All | "Did I get up fresh?" (optional) |

### Input Methods
- **Meal logging (adults):** calorie count manual entry, voice input (describe meal, AI parses), photo/barcode scan
- **Meal logging (kids):** 3-tap self-rating only
- **Movement:** manual entry (activity + duration) or calories burned
- **Hydration:** tap to add in ml increments
- **Add-on habits:** secondary section after core tracking — tap to log each

---

## 5. Add-On Library

Family picks up to 3 during onboarding. All members see and log them daily.

| Add-on | Detail (optional) |
|--------|------------------|
| Ate a fruit today | Which one |
| Ate vegetables today | Which one |
| Sugar check | Teaspoons |
| Took vitamins | — |
| Hit 10,000 steps | — |
| Alcohol-free day | — |
| Screen-free hour before bed | — |

Add-ons score points and appear on family leaderboard. Library grows based on what families actually pick.

---

## 6. Points System

| Action | Points |
|--------|--------|
| Hit calorie / eating habit goal | 10 |
| Hit movement goal | 10 |
| Hit hydration goal | 5 |
| Got up fresh | 5 |
| Each add-on completed | 5 |
| Day streak bonus | +2 per streak day |

- Max daily ~40–50 pts depending on add-ons selected
- Leaderboard shows **weekly points** — bad Monday doesn't kill the week
- **Family weekly score** = sum of all members
- Tracks against 90-day collective goal

---

## 7. The 90-Day Collective Goal

- System sets the target on the day the family is created
- Based on: number of members, their profile types (adult vs child), and max possible daily points
- Target is genuinely hard but achievable — approximately 70% of max possible over 90 days
- User cannot edit the target downward
- **Reward for hitting:** next quarter free — they stay in the app, keep the streak, become referral engine

---

## 8. Four Views

| View | Who sees it | Content |
|------|-------------|---------|
| My Dashboard | Every member | Personal calories, movement, streaks, goal progress |
| Family Dashboard | Every member | Leaderboard, digest, collective 90-day goal progress |
| Parent view of kids | Parent only | Kid streak + on track / off track. No raw numbers. |
| Admin | Parent only | Invite, family goal, add-ons, accountability toggle |

Solo tracking = My Dashboard only. Family layer is additive, never replaces personal view.

---

## 9. The 8pm Family Digest

Push notification at 8pm (configurable per family). No app-open required.

**Format:**
```
How did we do today?

The [Family Name] — Day 14

Vinos       ✅ Calories  ✅ Movement  ✅ Water   — 30 pts
[Spouse]    ✅ Calories  ⚪ Movement  ✅ Water   — 25 pts
[Child]     ✅ Active    ✅ Water     ✅ Veggies — 20 pts

Family today: 75 pts | Week: 420 pts | 90-day goal: 34% there

💬 [Child] is on a 6-day streak. Ask them about it at dinner.
```

**Conversation prompt:** AI-generated, personalised to actual family data. Uses streaks, misses, milestones, comparisons, weekly progress. Examples:
- "[Member] hit movement 5 days in a row — what's the secret?"
- "The family missed hydration today. Who's refilling the water jug tomorrow?"
- "Week 2 done. You're ahead of 68% of families at this stage."

AI model: Claude (Anthropic API). Prompt uses that day's family check-in data.

---

## 10. Visibility Modes

Three modes. Default is digest. Others discovered inside app.

1. **8pm digest** — default, always on, push notification
2. **Leaderboard** — weekly points, inside app
3. **Feed** — activity feed, inside app

---

## 11. Onboarding Flow (under 3 minutes)

**Step 1 — Parent sets up their own profile**
Height, weight, goal (lose / gain / maintain), food restrictions. BMI + daily calorie target calculated by system.

**Step 2 — Name your family + set family goal**
Family name + one tap:
- Get active together
- Build better eating habits
- Lose weight as a family

System sets 90-day target automatically from this point.

**Step 3 — Invite members**
Parent shares invite link or 6-character code (both supported).
- Each adult/teen member completes their own mini-onboarding on join
- Parent assigns child vs adult profile per invite
- Child accounts: parent sets up the child profile directly (name, age, movement goal, hydration goal — no calorie targets)

---

## 12. Invite & Auth Model

- Each adult/teen: own Supabase Auth login (email + password or magic link)
- Child accounts: no login — managed entirely by parent within the parent's session
- Invite methods: shareable link OR 6-character alphanumeric code
- Link/code expires after 7 days or first use (single-use per member slot)

---

## 13. Households + Guests

**Core household:** up to 6 members, paid plan

**Guests (free, invited by household):**
- See family leaderboard, digest, points and streaks — not personal calorie/weight data
- Can react to daily digest with emoji reactions only
- Cannot log their own data
- No limit on guest count
- When a guest reacts: household gets notification — *"Grandma reacted to Mia's streak ❤️"*
- Every guest is a warm lead — to log data they start their own Rally household

---

## 14. Pricing

| Plan | Price | Members |
|------|-------|---------|
| Monthly | $10/month | Up to 6 |
| Annual | $72/year (~$6/month) | Up to 6 |

**Mid-month joins:** prorated billing — charged only for remaining days in the current billing cycle.

**Reward for hitting 90-day goal:** next quarter free automatically applied.

**Payment:** Stripe. No per-seat pricing.

---

## 15. Design Assets (from Claude Design session, June 5)

Available in `~/Downloads/Vigor Family/`:
- Character sheets (avatar system, v1 + v2)
- Onboarding flows — profile, family setup, invite (two layout variants)
- 8pm digest screen designs (7 variants)
- JSX components for all screens
- Screenshots of all key states

These are the design source of truth for build.

---

## 16. Tech Stack

| Layer | Technology |
|-------|-----------|
| Mobile | React Native + Expo + TypeScript + NativeWind |
| Backend | Hono + TypeScript + Bun |
| Database + Auth | Supabase (separate project from solo Vigor) |
| AI (digest prompts) | Claude API (Anthropic) |
| Payments | Stripe |
| Push notifications | Expo Notifications |

---

## 17. MVP Scope (build in v1)

- [ ] Auth — parent login, child account management by parent
- [ ] Family creation + invite flow (link + code)
- [ ] Child vs adult profile types
- [ ] Core tracking — calories/macros (adults), eating habit self-rating (kids), movement, hydration
- [ ] Add-on library (7 options, family picks up to 3)
- [ ] Points system
- [ ] Family dashboard + weekly leaderboard
- [ ] 8pm digest push notification with AI-generated conversation prompt
- [ ] 90-day collective goal tracker (system-set on family creation day)
- [ ] Parent view of kids (on track / off track only)
- [ ] Guest access (read-only + emoji reactions)
- [ ] Stripe family plan + prorated mid-month join billing

---

## 18. Post-MVP (do not build in v1)

- Proof / accountability mode (photo required for meals)
- Custom add-ons (free-form) — library only for now
- In-app group chat
- Detailed child analytics for parents
- Social sharing outside family
- AI coaching
- Per-seat pricing

---

## 19. What Not To Build

- Do not make this a social network
- Do not add AI coaching in v1
- Do not let users set their own stretch targets
- Do not show raw calorie numbers for child profiles to parents
- Do not add per-seat pricing
- Do not compete with MyFitnessPal on features — compete on simplicity and the family ritual

---

## 20. Database Schema (to build in Supabase)

### Tables needed
- `profiles` — per user (adults/teens), mirrors solo Vigor structure
- `families` — family name, goal type, 90-day target, created_at
- `family_members` — links profiles to families, role (admin/adult/child), is_child boolean
- `child_profiles` — child-specific data (name, age, movement goal, hydration goal) — managed by parent
- `check_ins` — daily check-in per member (calories, movement, hydration, got_up_fresh, eating_habit_rating for kids)
- `addon_selections` — which 3 add-ons a family picked
- `addon_checkins` — daily add-on completions per member
- `points_log` — daily points per member (source breakdown)
- `digest_log` — daily digest sent, AI prompt used, conversation prompt generated
- `invites` — code + link, expiry, used_by, family_id
- `guests` — guest email/name, family_id, reactions

---

## 21. Marketing Anchors

- **Hero line:** "There is appetite to bring health into conversation — but no avenue."
- **Contrast:** Every other app makes tracking solo and tedious. Rally makes it a shared ritual.
- **The moment:** Your child asks at dinner — "Did you hit your water today? I got mine."
- **Category:** Rally owns "family health accountability" — no direct competitor
