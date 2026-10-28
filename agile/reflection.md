# Reflection — GrandCaddy Sprint

[← Back to portfolio](../)

---

The biggest thing I learned this sprint is that the team's speed depended on mine. Luke couldn't wire sign-up to Supabase Auth until the `users` table existed, and Rocco couldn't build the helper form until `helper_profiles` and `bookings` were live. I didn't treat "backend first" as a priority at the start — I treated it as a preference. It's not. Every hour the tables weren't there was an hour three people were blocked.

Writing the brief for Luke and Rocco was harder than I expected. My first draft was basically "here are the columns, good luck." Rocco came back asking which fields were required and whether a Helper sign-up creates a `users` row as well as a `helper_profiles` row — I'd assumed that was obvious and it wasn't. What fixed it was adding a realistic example row to each table in the brief. Once Rocco could see a filled-in `helper_profiles` row, the form built itself. What I missed entirely was the task status lifecycle — I wrote "open, accepted, completed" and Luke asked what happens if a helper accepts and then abandons a task. I still haven't handled that state. That's a design miss, not a coding miss, and it would have taken ten minutes to think through up front.

On the sign-up: I built the pages, Luke wired the form to Supabase Auth including the Customer/Helper toggle. I wired the login page myself early on, which is why it was already working when Luke picked up sign-up. The toggle was the tricky bit — a Helper sign-up has to insert into `users` and `helper_profiles` in the right order, and if the second insert fails the first shouldn't be left dangling. I didn't specify that in the brief; Luke solved it himself. In a real project I'd have written it down.

I want to be honest about one weakness. The brief tells Rocco to use "Public all" development policies, which means anyone holding the app's public anon key can read or write his tables freely. That's fine for building fast in a sprint, but the anon key ships inside the frontend bundle — anyone who opens DevTools can grab it and modify other people's bookings. Before this app goes near real users, every table needs Row Level Security policies checking `auth.uid()` against the row owner. That's probably a full sprint on its own, and I'd rather name it clearly here than pretend the app is production-ready.

If I did this again I'd write the task status lifecycle before the brief, add one smoke test for the sign-up flow early, and deploy to Vercel on day two so a broken build late in the sprint isn't a crisis.

Third year is a strange place — you know enough to build something real, and not enough to know all the ways it can break. The orphaned auth row, the missing state, the public key gap: those don't show up in tutorials. They show up when you ship. I'm taking that as the lesson.

---

## Related pages

- [Sprint Overview](sprint-overview.md) — team, timeline, and what we scoped out
- [Backlog](backlog.md) — the Trello board and story acceptance criteria
- [Evidence](evidence.md) — Local History, commits, Supabase, Vercel, and the briefs
