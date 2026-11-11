# RichMindStreet Trading Journal — Mobile PWA

A mobile-first, installable Progressive Web App. No server, account, or cloud database is used. Trade data is stored locally in the browser.

## Run locally
Serve this folder from a local web server (service workers require HTTPS or localhost):
- `python3 -m http.server 8000`
- Open `http://localhost:8000`

## Deploy
Upload the contents of this folder to a static HTTPS host such as GitHub Pages. The app is installable from the browser's "Add to Home Screen" / "Install app" option.

## Included
- Dashboard for the ₹30,000 → ₹1,00,000 challenge
- Lot calculator with lot size choices 65, 10, and 20
- Entry, stop-loss, target, direction and point-value multiplier
- Minimum RR validation and floor-based lot sizing
- Trade log with open/closed status and actual net P&L
- Win/loss/break-even classification, trade review notes
- Analytics: win rate, net P&L, expectancy, net R, profit factor and daily P&L
- Local settings, JSON backup/restore and reset
- Offline shell caching via service worker

## Challenge rules implemented
- Starting capital: ₹30,000; target: ₹1,00,000
- First trade risk budget: ₹1,500
- Subsequent risk budget: 10% of cumulative net realized P&L, provided it is positive
- Minimum risk/reward: 1:1
- Reject if one lot exceeds the risk budget
- Stop after two consecutive losses; pause if cumulative realized P&L is zero or negative

## Calculation
- Risk per lot = `abs(entry - stop loss) × lot size × point value multiplier`
- Reward per lot = `abs(target - entry) × lot size × point value multiplier`
- RR = `reward per lot / risk per lot`
- Lots = `floor(risk budget / risk per lot)`

The multiplier defaults to 1 and is editable because contract multipliers/point values vary by instrument and contract. Verify current exchange contract specifications before trading.

## Local storage warning
Clearing browser/site data can erase the journal. Export JSON backups regularly. Importing a backup replaces current local journal data.
