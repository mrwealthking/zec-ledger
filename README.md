# ZEC Ledger

A lightweight, single-file web app for tracking Zcash transparent-address activity as a running accounting ledger — built for the ZecHub 2026 Hackathon (**Accounting** track).

**Live mainnet data. No backend. No build step. No wallet keys required.**

## What it does

Enter any Zcash **transparent address** (`t1...` / `t3...`) and ZEC Ledger:

- Fetches the address's real transaction history directly from the **Zcash mainnet**, via the public [Blockchair](https://blockchair.com/zcash) explorer API.
- Displays current balance, total received, total sent, and transaction count.
- Builds a full **running-balance ledger** — every transaction in chronological order, with the balance after each one, similar to a bank statement.
- Lets you **export the ledger as a CSV file** for bookkeeping, tax prep, or personal record-keeping.

This is genuinely useful for anyone accepting ZEC for a business, tracking a public donation address, or just wanting a clean accounting view of a transparent address without running their own node or pasting addresses into a third-party tracker that may log queries.

## Why this matters

Zcash's transparent pool is fully public on-chain — but there's no lightweight, open-source tool that turns that raw transaction data into something that looks and feels like an actual ledger a small business or individual could use for basic accounting. ZEC Ledger fills that specific gap:

- **Privacy-respecting by default**: shielded transactions are never shown or queried, since they're private by design — this tool only ever surfaces already-public transparent-address data.
- **No signup, no backend, no server costs**: it's a static HTML file that runs entirely in the browser.
- **Real mainnet interaction**: not a mockup — every number shown is a live read from the Zcash blockchain.

## How it works

1. You enter a transparent Zcash address.
2. The app calls Blockchair's public API (`api.blockchair.com/zcash/dashboards/address/{address}`) to get the balance, totals, and list of transaction IDs.
3. It fetches full details for each transaction (`api.blockchair.com/zcash/dashboards/transactions/{txid1},{txid2},...`, batched 10 at a time), works out how much that address sent or received in each one, sorts everything chronologically, and computes a running balance across the address's entire history.
4. Everything renders client-side — no data is stored, sent to a third-party server, or logged by this app.

## Usage

**Option A — just open it:**
Download `index.html` and open it directly in any modern browser. No installation needed.

**Option B — host it (e.g. GitHub Pages):**
1. Push this repo/folder to GitHub.
2. Enable GitHub Pages for the repo (Settings → Pages → deploy from the `main` branch).
3. Visit the generated `https://<username>.github.io/<repo>/` URL.

## Example

Try it with any known public Zcash transparent address (e.g. a mining pool payout address or a public donation address) to see real transaction history populate immediately.

## Tech stack

- Vanilla HTML/CSS/JavaScript — zero dependencies, zero build tools.
- [Blockchair public API](https://blockchair.com/api/docs) for live Zcash mainnet data.

## Limitations / honest notes

- Only supports **transparent addresses** — shielded (`z...`/`u...`) addresses are private by protocol design and cannot be queried this way, which is intentional and correct behavior for a privacy coin.
- Relies on Blockchair's public API uptime and rate limits (free tier: 1,000 calls/day, no key required); a production version could add support for multiple explorer backends as a fallback.
- Pagination is currently capped at the most recent 100 transactions per address; very high-activity addresses would need a "load more" feature to see full history.

## License

MIT — see [LICENSE](./LICENSE).

## Track

**Accounting** — ZecHub 2026 Hackathon
