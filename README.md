# Instarem Fund by Card Miles Calculator

A single-page calculator that shows how many KrisFlyer miles a business earns by paying through Instarem Fund by Card with an SG-issued Visa card, and what each mile costs.

Everything lives in one file, `index.html`. The card images and the HeyMax logo are built into the file, so there are no other assets to upload.

## Features

### Tab 1: Miles calculator
- Enter the total payment amount and the service charge (1.5% to 2.5%).
- Tick one or more Visa cards and enter how much goes on each card.
- Results:
  - total KrisFlyer miles and miles per S$1
  - cost per mile, with a Great, Fair or Pricey rating
  - service charge and total you pay
  - a per-card breakdown
- **Trip reference:** the first flight the miles can cover, with the destination's flag, e.g. "Return to Japan · Economy".
- **Compare cards:** a collapsible table at the bottom that runs each card against the full amount.
- **Mobile:** a sticky bar at the bottom of the screen shows total miles and cost per mile.

### Tab 2: HeyMax bonus
- Awards 20,000 HeyMax Max Miles for every full S$50,000 paid with Fund by Card.
- Inputs: transaction amount (multiples of S$50,000 only) and average miles per S$1.
- The table shows regular miles next to regular miles plus Max Miles combined.

## How the calculation works

| Item | Rule |
|---|---|
| Miles | Payment amount × card rate, rounded down to the issuer's earning block (e.g. per S$5 for DBS and UOB). |
| Service charge | Paid to Instarem on top of the payment. It does not earn miles and does not count towards card caps. |
| Cost per mile | Service charge ÷ miles earned. |
| Card eligibility | Each card is checked against the Instarem MCC list. A card is listed only if it earns at least 1 mpd on those MCCs. MCCs are never shown on the page. |
| Trip reference | KrisFlyer Saver one-way prices from Singapore; Return = 2 × one-way. The US is checked first, then France, Japan, China, Hong Kong and Malaysia. Within a destination, Business is shown before Economy, then Return before One-way. Hidden below 8,000 miles. |
| HeyMax bonus | `floor(amount ÷ 50,000) × 20,000` Max Miles, added to `amount × average mpd`. |

## Cards included

| Card | Rate | Earning block |
|---|---|---|
| UOB Reserve Visa Infinite | 1.6 mpd | S$5 |
| OCBC Premier VOYAGE | 1.6 mpd | S$1 |
| DBS Vantage Visa Infinite | 1.4 mpd (from Nov 2026) | S$5 |
| OCBC VOYAGE | 1.4 mpd | S$1 |
| UOB PRVI Miles Visa | 1.4 mpd | S$5 |
| UOB Visa Infinite Metal | 1.4 mpd | S$5 |
| DBS Altitude Visa Signature | 1.3 mpd | S$5 |
| OCBC 90°N Visa | 1.3 mpd | S$1 |

Not included:
- Maybank and Standard Chartered cards (earn rates cut)
- HSBC cards
- Citi Rewards (the Visa version was discontinued in October 2026)
- UOB Preferred Platinum and UOB Visa Signature: they stay in the data but are hidden, because their bonus categories don't cover the Instarem MCCs.

## Updating the data

All settings sit at the top of the second `<script>` block in `index.html`.

| What to change | Where |
|---|---|
| Card rates, caps, earning blocks | `CARDS` |
| Instarem MCC list | `INSTAREM_MCCS` |
| MCCs that earn no points | `COMMON_EXCLUDED` |
| Bonus-category MCC lists | `MCC` |
| KrisFlyer award prices and destination order | `AWARDS` |
| HeyMax block size and bonus | `HM_BLOCK`, `HM_BONUS` |
| Minimum rate to list a card | `MIN_MPD` |
| Cost-per-mile rating bands | `CPM_GOOD`, `CPM_FAIR` |
| Service charge range | the `fee` slider's `min`, `max` and `value` in the HTML |

To add a card, add an entry to `CARDS`. Without an `image`, the card shows a coloured placeholder made from `colors`. To add card art, put a small base64 PNG into `CARD_IMAGES` (first `<script>` block) and point the card's `image` at it.

## Deploying (Vercel via GitHub)

1. On github.com, open this repository and choose **Add file → Upload files**.
2. Drag in `index.html` (and this `README.md`) and click **Commit changes**.
3. If the repository is connected to Vercel, it redeploys automatically. To connect it the first time, go to Vercel and choose **Add New → Project**, import the repository, keep the default settings and click **Deploy**.

No build step or dependencies are needed. Vercel serves `index.html` as a static page.

## Before going live

- [ ] Check every card's rate, cap, earning block and Visa status with the issuer.
- [ ] Confirm the bonus-card MCC lists against the issuers' latest terms.
- [ ] Check the KrisFlyer Saver prices in `AWARDS`, especially France and the US, which use zone prices.
- [ ] Get approval to use the banks' card images and the HeyMax logo.
- [ ] Confirm the HeyMax bonus terms (20,000 Max Miles per S$50,000).

## Disclaimer

For reference only. The estimates for air miles are based on publicly available data and are provided for informational purposes only. Miles shown are KrisFlyer miles. Earn rates, award prices and eligibility may change.
