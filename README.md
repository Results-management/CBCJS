# School Results App

Adapted from the same base app, with one structural change: **CRE renamed to
RE** (Religious Education), since learners follow either CRE or IRE.

Every subject is scored as a single mark out of 100, for both Mid Term and
End Term assessments. Every learner also has an **Assessment Number**, set
when they're registered, editable anytime, and shown on the report card,
class list, and every export.

Everything else — single-stream or multi-class grades, School Settings,
Manage Classes, Year Advancement Wizard, Excel/CSV, Results Analysis (now
printable and downloadable as a PDF) — works as described below.

## Files
- `index.html` — the whole app
- `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png` — installable home-screen app (PWA)
- `db.json` — empty starting database

## Upload to GitHub Pages
1. Create a new **public** repo.
2. Upload all six files to the repo root, on the `main` branch.
3. Settings → Pages → Deploy from branch → `main` / `root`.

## First-time setup
1. Open the site → **Database Settings** → enter your GitHub owner, repo name,
   and a Personal Access Token (`repo` scope).
2. Log in: username `admin`, password `admin2026`. **Change this immediately**
   under ✏️ Manage Team.
3. Go to **🏫 School Settings** and fill in your school's header exactly as
   you want it to print — School Name, P.O. Box, County, Motto, Phone, Email.
   Leave any field blank to leave it off the header entirely. This appears on
   the login screen, class lists, and report cards:

   ```
   YOUR SCHOOL NAME
   P.O BOX 32 - 80120
   YOUR COUNTY
   Motto: Hard Work Pays
   0712 345 678 · info@yourschool.ac.ke
   ```

4. Go to **🏫 Manage Classes** to set up your grades — add as many named
   classes per grade as you need (or leave the single default "Main" class
   per grade if you don't split streams).
5. Go to **✏️ Manage Team** to set up real logins for your class teachers
   and rename the subject-teacher placeholder accounts below.

## Logins (change all of these before going live)
| Login | Username | Password | Covers |
|---|---|---|---|
| Admin | `admin` | `admin2026` | Everything |
| Mathematics | `mathematics` | `math2026` | Grades 7–9 |
| English | `english` | `eng2026` | Grades 7–9 |
| Kiswahili | `kiswahili` | `kis2026` | Grades 7–9 |
| Integrated Science | `science` | `sci2026` | Grades 7–9 |
| Pre-Technical Studies | `pretechnical` | `pts2026` | Grades 7–9 |
| Agriculture & Nutrition | `agriculture` | `2026agric` | Grades 7–9 |
| Social Studies | `socialstudies` | `ss2026` | Grades 7–9 |
| RE (Religious Education) | `re` | `re2026` | Grades 7–9 |
| Creative Arts & Sports | `creativearts` | `cas2026` | Grades 7–9 |
| Class Teacher, Grade 7/8/9 | `classteacher7`/`8`/`9` | `2026` | One grade each |

## Registering learners
Every learner has two identifying fields: **Assessment Number** (their
admission/exam number) and **Full Name**. Both are set when you add a
learner, and both can be edited later:
- **+ Learner** button on the results screen (class teacher / admin)
- **Edit** on any learner's row (opens Assessment No., Name, and marks — all editable)
- During the **Year Advancement Wizard**, when registering a new Grade 7 intake
- Via **CSV/Excel import** — include an "Assessment No." column alongside Name

Assessment Numbers carry forward automatically when a class is promoted a
grade via the Year Advancement Wizard.

## What every role can do
- **Admin** — everything: connect the database, School Settings, Manage
  Classes, Manage Team, Year Setup, all downloads/prints.
- **Class Teacher** — their assigned grade only: register/edit learners,
  enter marks for any subject if needed, comments, print/download, CSV/Excel.
- **Subject Teacher** — any class, their one subject: marks entry (with
  Assessment Numbers shown for reference), grade distribution, print/download
  for that subject's data.

## Downloads, printing, and analysis
- **⬇ Download buttons produce real PDF files** (via a client-side PDF
  generator), for the blank class list, results list, all report forms, and
  individual report cards. "All Report Forms" for a full class can take a
  few seconds — the button shows "Generating PDF…" while it works.
- **🖨 Print buttons** open the browser's print dialog as an alternative —
  also lets you choose "Save as PDF" there if you prefer.
- **📊 Results Analysis** — overall distribution, class mean, pass rate,
  per-subject grade distribution and means, and a Top 5 performers list.
  Has its own 🖨 Print and ⬇ Download PDF buttons.
- **Excel and CSV** exports/imports include Assessment No., Name, and one
  column per subject, so you can prepare marks offline in the same format.

## Notes
- **Fixed a real paper-waste bug**: report cards were forcing one card per
  printed page even though each card only fills part of a page — so a class
  of 30 was printing 30 pages with a lot of wasted blank space. That forced
  break is removed. Each report card is guaranteed to be **more than half a
  page** (a firm height floor, well over half of A4), so it always looks
  substantial and never gets awkwardly split across a page break — it just
  no longer forces a needless extra blank page after itself. Applies to both
  the 🖨 Print and ⬇ Download PDF paths.
- Data lives in `db.json` in your GitHub repo — every teacher's device stays
  in sync automatically as long as they're connected.
- Never share your GitHub Personal Access Token outside the app's own
  Database Settings screen.
- One GitHub repo = one school. This is a separate deployment from any other
  school's app — its own repo, its own data, its own School Settings.
- After uploading an update to `index.html`, clear site data once (or check
  in a private/incognito tab) — the app caches itself for offline use, so a
  stale cached copy can otherwise keep showing until that's cleared.
