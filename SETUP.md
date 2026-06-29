# Arya's Playbook — Setup

A single-file training app for GAA football, Camogie, agility and running.
Same stack as Bubbli: one `index.html`, Firebase **Anonymous Auth + Realtime Database**
loaded from the CDN, deployed on **GitHub Pages**. No build step.

You and Arya both open the same web page and enter the **same Space Code**, so the
plan you build on your phone shows up live on hers, and the sets/runs/tests she logs
sync straight back to you.

---

## 1. Create a Firebase project (5 min)

> Use a **NEW** project — don't reuse Bubbli's, so the data and security rules stay separate.

1. Go to <https://console.firebase.google.com> → **Add project** (e.g. `arya-playbook`).
   You can skip Google Analytics.
2. In the project, click the **Web** icon (`</>`) to register a web app. Give it any
   nickname. **Don't** enable Hosting (we use GitHub Pages). Copy the `firebaseConfig`
   object it shows you — you'll paste it in step 4.
3. **Build → Authentication → Get started → Sign-in method → Anonymous → Enable.**
4. **Build → Realtime Database → Create database.**
   - Pick the **europe-west1** location (closest to Ireland).
   - Start in **locked mode** (we'll paste rules next).

## 2. Paste the security rules

In **Realtime Database → Rules**, replace everything with the contents of
[`database.rules.json`](database.rules.json), then **Publish**.

These rules say: any signed-in user (anonymous counts) can read/write under `spaces/`.
That's fine for a private family app behind an obscure project + space code.

## 3. Paste your Firebase config

Open `index.html`, find the block marked **`PASTE YOUR FIREBASE CONFIG HERE`**
(near the bottom, in the `<script>`), and replace the placeholder `firebaseConfig`
object with the one you copied in step 1. Make sure `databaseURL` is included.

## 4. Deploy on GitHub Pages

Same as Bubbli:

1. Create a repo (e.g. `arya-playbook`) and push `index.html` to it.
2. **Settings → Pages → Build from branch → `main` / root → Save.**
3. After a minute it's live at `https://<you>.github.io/arya-playbook/`.

## 5. First run

1. Open the page on **your** phone. Enter:
   - **Athlete name** (Arya)
   - **Space code** — anything you both will type, e.g. `arya-gaa`
   - **Coach PIN** — a 4-digit code that unlocks Coach mode (default `1234`)
2. The week plan, skills library and baseline tests are seeded automatically the first time.
3. On **Arya's** phone, open the same page and enter the **same space code** (she does
   not need the PIN — that's only for editing). In Safari, tap **Share → Add to Home
   Screen** so it opens full-screen like an app.

## Using it

- **Today** — her plan for each day. She ticks off each set as she does it.
- **Run** — a big stopwatch to time the 3.6 km run; logs time + pace, charts progress.
- **Tests** — the pre/post agility baseline tests (sprint, 5-10-5, broad jump…). Record a
  **Pre** result now, train the block, then a **Post** result to see the improvement.
- **Progress** — weekly completion, run trend, test improvements, and the coach/safety notes.
- **Coach** (🔒 PIN) — you build/edit the week, add skills, paste real YouTube links, edit
  tests, and back up/restore the data.

## Notes

- Every skill links to a YouTube **search** (always works). In Coach mode you can paste a
  specific video URL for any skill to make it one-tap.
- "Re-seed defaults" in Coach mode restores the original plan/skills if you want a clean slate.
- Back up anytime with **Export** in Coach mode (downloads a JSON file).
