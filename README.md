# BOH PTO Calendar

A shared calendar for tracking kitchen team time off. Days where too many people from the same position group are off turn red, so you don't approve overlapping PTO.

**Live app:** https://arlo-b213.github.io/pto/

## Passcodes
- **Editor** – add, edit, approve and delete time off; change limits and the team roster.
- **View only** – see the calendar.

Passcodes are stored as SHA-256 hashes in `index.html` (`const PASS`). To change one, hash the new passcode and replace the value.

## First-time setup
1. **Firestore database** – In the Firebase console for project `boh-pto`, open *Build → Firestore Database* and create a database (production mode is fine).
2. **Rules** – Open the *Rules* tab, paste the contents of `firestore.rules`, and click *Publish*.
3. **Load your team** – Open the app, enter the editor passcode, click *Limits & team → Import starter file*, and choose `pto-starter.json` (kept out of this public repo on purpose).

## How limits work
Each position group has a daily limit (most people off on one day), plus one limit for the whole kitchen. A day at the limit shows **FULL**; a day over it shows **OVER LIMIT** and is listed under *Conflicts ahead*. Change limits under *Limits & team*.

## Files
- `index.html` – the app
- `firebase-config.js` – Firebase project settings
- `firestore.rules` – database rules to paste into Firebase

Note: the passcode screen keeps casual visitors out, but it isn't strong security. Don't store anything sensitive in this app.
