# Sprint Backlog — GrandCaddy

[← Back to portfolio](../)

---

## 1. Overview

The sprint backlog is maintained in Trello, where each story is a card with an owner, acceptance criteria, and a status. The board was updated throughout the sprint — cards moved from "To Do" to "In Progress" to "Done" as work was completed, not after the sprint ended. A screenshot of the board is below, followed by a summary of the nine stories and how they were split across the three team members.

---

## 2. The board

![GrandCaddy Sprint Backlog — Trello board showing To Do, In Progress, and Done columns](../assets/evidence/trello-board.png)

> The board is currently workspace-private. A live link will be added once visibility is changed to public. The screenshot above shows the full board as it stood at the end of the sprint.

---

## 3. How the board was used

Cards were created **before** work started, not after. Luke's and Rocco's cards were written from the briefs I gave them (see the [Evidence page](evidence.md)), so each card's description matched what they were actually asked to build.

Cards moved between lists as work progressed: **To Do → In Progress → Review → Done.** The "Review" list existed because integration bugs — the auth flow, status propagation — were found after a story *looked* finished. Moving the card back to "Review" made that visible rather than hiding it.

Two cards stayed in "In Progress" at the end of the sprint: delivery tracking and cancellation handling. Both are listed as deferred in the [Sprint Overview](sprint-overview.md) under "What we scoped out." They're not forgotten — they're the next sprint's work.

---

## 4. Story summary

| # | Story | Owner | Status |
|---|---|---|---|
| 1 | Visitor understands the service | Isaac | Done |
| 2 | User creates an account and logs in | Isaac / Luke | Done |
| 3 | Customer posts and tracks a task | Isaac / Luke | Done |
| 4 | Helper signs up | Rocco | Done |
| 5 | Helper finds and accepts a task | Rocco | Done |
| 6 | Helper completes work | Rocco | Done |
| 7 | Customer sees task status updates | Isaac | Partly done (delivery tracking deferred) |
| 8 | Admin posts announcements | Isaac | Done |
| 9 | Everyone can use the live site | Isaac | Done |

**Legend:** Done = acceptance criteria met and tested. Partly done = core path works, deferred features listed on the [Sprint Overview](sprint-overview.md) page.

---

## 5. Acceptance criteria

The full acceptance criteria for each story are in the Trello card descriptions. For reference, the acceptance criteria for the two most important stories are below.

### Story 2 — User creates an account and logs in

- Sign-up form accepts email, password, and role (Customer or Helper).
- On submit, a row appears in `auth.users` and a matching row in `public.users` with the correct `role`.
- If the role is Helper, a row also appears in `helper_profiles` with `verification_status = 'pending'`.
- If the second insert fails, the first is rolled back — no orphaned users.
- Login redirects Customer to `/` and Helper to `/browse-tasks`.
- Invalid credentials show an error message, not a silent failure.

### Story 5 — Helper finds and accepts a task

- Browse Open Tasks fetches only `status = 'open'` tasks.
- Each card shows category, title, suburb, offered amount, preferred date.
- Accept button only visible to logged-in helpers (users with a `helper_profiles` row).
- Clicking Accept inserts a row into `bookings` (`task_id`, `helper_id`, `status = 'accepted'`) **and** updates the task to `status = 'assigned'` with `assigned_helper_id` = helper's id.
- If either write fails, neither is committed.
- After accepting, redirect to `/helper/bookings`.

---

## 6. Deferred items

| Item | Reason deferred |
|---|---|
| Delivery tracking with delay updates | Needs a separate `deliveries` table and a helper-side form — its own sprint |
| Row Level Security on `helper_profiles` and `bookings` | Currently `Public all` for development speed (see [Reflection](reflection.md) for full explanation) |
| Cancellation flow (helper accepts then abandons) | State machine only covers `open → assigned → completed`; no `cancelled` path yet |
| Forgot password flow | Listed as optional in Luke's brief, not built |
| Search across tasks | Browse filters by category only; no text search yet |

---

## 7. Evidence

Full evidence for the sprint — Local History, commit history, Supabase table screenshots, Vercel screenshots, and the briefs — is on the [Evidence page](evidence.md).
