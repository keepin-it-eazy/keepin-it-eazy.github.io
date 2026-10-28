# Sprint Overview — GrandCaddy

[← Back to portfolio](../)

---

## 1. What the sprint was

GrandCaddy is a task marketplace for the CPUT community. Customers post tasks they need done — moving furniture, fixing a tap, tutoring a first-year, walking a dog — and helpers accept them for an agreed price. The app was built over a single sprint from **7 August to 25 October 2026** by a three-person team: Isaac (backend, auth, deployment), Luke (customer experience), and Rocco (helper experience).

The sprint goal was: **a customer can sign up, post a task, and track it; a helper can sign up, browse open tasks, accept one, and mark it complete — all on a live deployment backed by Supabase.**

---

## 2. Team and roles

| Person | Role | What they owned |
|---|---|---|
| Isaac | Lead / Backend | Schema (`users`, `tasks`, `task_categories`, `announcements`, `reviews`), auth pages, home page, Vercel deployment, briefs for Luke and Rocco |
| Luke | Customer experience | Sign-up wired to Supabase Auth (Customer/Helper toggle), Post-a-Task form, My Tasks, Task Detail, shared TaskCard component |
| Rocco | Helper experience | `helper_profiles` and `bookings` tables, Helper Signup, Browse Open Tasks, Accept Task, My Bookings with Mark Complete |

---

## 3. Sprint at a glance

| Metric | Value |
|---|---|
| Sprint length | 7 August – 25 October 2026 |
| Team size | 3 |
| Stories committed | 9 |
| Stories fully done | 8 |
| Stories partly done | 1 (delivery tracking — see section 5) |
| Live site | [grand-caddy.vercel.app](https://grand-caddy.vercel.app) |
| Backlog | [Trello board](https://trello.com/b/0Xkqcaec/grandcaddy) (or see [Backlog page](backlog.md)) |

---

## 4. How the sprint was structured

The sprint was split by role, not by layer. Isaac owned the backend and the pieces that everyone else depended on: the database schema, the auth pages, and the deployment. Luke and Rocco owned the two user journeys — customer and helper — which run in parallel once the tables exist.

This meant the dependency order was deliberate:

1. **Tables first** (`users`, `tasks`, `task_categories`) — because Luke couldn't wire sign-up without `users`, and couldn't build Post-a-Task without `tasks`.
2. **Briefs second** — written from the finished schema, so Luke's and Rocco's cards matched the tables they were building against.
3. **Pages third** — Luke and Rocco built in parallel once their tables and briefs were ready.
4. **Deployment last** — the only task nobody else depends on, so it went at the end.

The reason this mattered: every hour the tables weren't there was an hour three people were blocked. Backend-first wasn't a preference — it was the critical path.

---

## 5. What we scoped out

Not everything in the original brief made it into this sprint. These were deliberately deferred, not forgotten:

- **Delivery tracking with delay updates** — the brief describes a task moving through "delivered on 5 November @ 15:00" and updating if delayed. The current app shows the task's `preferred_date` but doesn't have a separate delivery estimate that can be updated by the helper. This needs its own `deliveries` table and a helper-side form.
- **Row Level Security on `helper_profiles` and `bookings`** — both tables currently use `Public all` development policies. Before real users, every table needs policies checking `auth.uid()` against the row owner. This is a known trade-off made to keep the team moving during the sprint (see the [Reflection](reflection.md) and [Logbook](backlog.md) for the full explanation).
- **Cancellation flow** — the task state machine only covers `open → assigned → completed`. There's no path for a helper who accepts and then abandons.
- **Forgot password** — listed as optional in Luke's brief and not built.
- **Search across tasks** — the browse page filters by category only; no text search yet.

Naming what's missing is what separates a scoped sprint from an unfinished one. A lecturer reading this knows exactly what was built and what wasn't, and can see that the decisions were made on purpose.

---

## 6. Evidence

All evidence for this sprint is collected in the [`assets/evidence/`](../assets/evidence/) folder and referenced in the [Evidence page](evidence.md). Summary:

- **Local History** — first code save 7 August 2026
- **Commit history** — 4 project commits on `main`, latest 14 October 2026
- **Supabase** — table screenshots for `users`, `tasks`, `task_categories`
- **Vercel** — live site screenshots of home, login, sign-up
- **Briefs** — Luke's and Rocco's task briefs
- **Backlog** — Trello board screenshot

---

## 7. Full reflection

The full reflection on what I learned, what I'd do differently, and the weakness I'd address before real users is on the [Reflection page](reflection.md).
