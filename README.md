# BOH PTO Calendar

A shared calendar for tracking kitchen team time off. Days where too many people from the same position group are off turn red, so you don't approve overlapping PTO.

**Live app:** https://arlo-b213.github.io/PTO/

## Passcodes
- **Editor** – add, edit, approve and delete time off; change limits and the team roster.
- **View only** – see the calendar.

Passcodes are stored as SHA-256 hashes in `index.html` (`const PASS`). To change one, hash the new passcode and replace the value.

## First-time setup
1. **Firestore database** – In the Firebase console for project `boh-pto`, open *Build → Firestore Database* and create a database (production mode is fine).
2. **Rules** – Open the *Rules* tab, paste the contents of `firestore.rules`, and click *Publish*.
3. **Load your team** – Open the app, enter the editor passcode, click **Import schedules**, and choose your weekly schedule files (e.g. `10052026_Schedule_2026.xlsx`). You can select several weeks at once.

## Importing weekly schedules
- Reads the first sheet of each weekly schedule: names in column A, badge in B, Mon–Sun in C–I, dates in row 2.
- Cells marked **PTO** (or VAC) become PTO; **LOA** becomes Leave. Consecutive days are merged.
- Section headers set each person's group: Chef, Assistant Chef, Sous Chef, AM Line Cooks, the unlabeled block after AM (PM Line Cooks), Swing & Late Swing, Grave.
- **Roster sync:** the team list is replaced to match the newest week you import — new hires are added, people no longer on the schedule are removed, and group moves are applied. You see every change before you apply it. Importing an older week never changes the roster.
- Re-importing a week replaces that week's imported time off. Time off entered by hand in the app is never touched, and a person is only counted once per day.

## How limits work
Each position group has a daily limit (most people off on one day), plus one limit for the whole kitchen. A day at the limit shows **FULL**; a day over it shows **OVER LIMIT** and is listed under *Conflicts ahead*. Change limits under *Limits & team*.

## Files
- `index.html` – the app
- `firebase-config.js` – Firebase project settings
- `firestore.rules` – database rules to paste into Firebase

Note: the passcode screen keeps casual visitors out, but it isn't strong security. Don't store anything sensitive in this app.
