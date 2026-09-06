════════════════════════════════════
  CHROMR WIN — APP INSTALLATION
════════════════════════════════════

FILES IN THIS PACKAGE:
  color-bet-game.html  ← Main game file
  manifest.json        ← PWA manifest
  sw.js                ← Service worker (offline support)
  icon-192.png         ← App icon (small)
  icon-512.png         ← App icon (large)

════════════════════════════════════
STEP 1 — ADD YOUR SUPABASE KEYS
════════════════════════════════════
Open color-bet-game.html in any text editor.
Find these 2 lines and replace with your real keys:

  const SURL='https://YOUR_PROJECT.supabase.co';
  const SKEY='YOUR_ANON_KEY';

════════════════════════════════════
STEP 2 — HOST THE APP
════════════════════════════════════
Upload ALL 5 files to the SAME folder on your server:
  - Netlify (free): drag & drop folder at netlify.com/drop
  - GitHub Pages (free)
  - Any web hosting

ALL files must be in same directory for PWA to work.

════════════════════════════════════
STEP 3 — INSTALL ON PHONE
════════════════════════════════════
Android (Chrome):
  1. Open your site URL in Chrome
  2. Tap menu (⋮) → "Add to Home Screen"
  OR tap the "📲 Install App" button that appears

iPhone (Safari):
  1. Open your site URL in Safari
  2. Tap Share (□↑) → "Add to Home Screen"
  3. Tap "Add"

════════════════════════════════════
BONUS: CHANGE SIGNUP BONUS
════════════════════════════════════
Search in color-bet-game.html:
  const BONUS=50          ← signup bonus (₹50)
  const MIN_DEP_FOR_WD=100 ← min deposit to withdraw

════════════════════════════════════
