# Armando's Inventory Tracker

A shared inventory + sales tracker for the electronics resale business.
Runs as a single static page, backed by Firebase Realtime Database so you
and your wife see the same live data on separate phones.

## What it does
- Add inventory items (SKU, rack, cost, condition, notes)
- Scan a QR code label with your phone camera to pull up an item and mark it sold
- Records cost, sold price, profit, platform, and date automatically
- Full undo on any sale (restores the item to stock)
- Activity log of every add / sell / delete / undo, timestamped
- Live sync — both phones read and write the same database

## 1. Lock down your Firebase database (do this first)

Your database is currently in test mode, which means anyone with the URL can
read or erase your data. Fix this now:

1. Go to https://console.firebase.google.com → your `armando-inventory` project
2. Build → Realtime Database → **Rules** tab
3. Replace the rules with the contents of `database.rules.json` in this folder
4. Click **Publish**

This requires a signed-in user (the app signs in anonymously and automatically —
you don't see a login screen, it just happens in the background) before any
read or write is allowed. It's not perfect security (anyone with your exact
URL could still open the app and get an anonymous session), but it stops
random bots and search-engine crawlers from wiping your database, which is
the real risk with test mode.

If you want it locked to just you and your wife specifically, tell me and
I'll swap anonymous auth for email/password — a bit more setup but tighter.

## 2. Push to GitHub

```bash
# From this folder:
git init
git add .
git commit -m "Inventory tracker v1"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/armando-inventory.git
git push -u origin main
```

(Create the empty repo on github.com first, don't initialize it with a README there.)

## 3. Enable GitHub Pages

1. On the repo page: Settings → Pages
2. Source: **Deploy from a branch**
3. Branch: `main`, folder: `/ (root)`
4. Save

Your app will be live in a minute or two at:
`https://YOUR_USERNAME.github.io/armando-inventory/`

Bookmark that URL on both your phone and your wife's phone.

## Notes
- Camera scanning needs HTTPS — GitHub Pages provides this automatically, so it'll work.
- If the camera doesn't prompt for permission, check your phone's browser site settings.
- The `apiKey` in the HTML is meant to be public in Firebase's model — your actual
  protection is the database rules from step 1, not hiding this key.
