# ArbScan LIVE

A live DEX arbitrage tracker (real prices via GeckoTerminal) with a MetaMask
connect button and a **simulated** combo-execution flow.

Important: **"Execute Combo" is a simulation only.** It does not send any
real transaction, swap, or flash loan — no matter what network you deploy
this to. The wallet connection is real (address / network / balance), but
nothing in this app moves funds.

## Why you need to deploy this at all

MetaMask (desktop extension or mobile app) only injects `window.ethereum`
into a real, top-level page it navigates to. It will not inject into a
sandboxed iframe — which is how Claude artifact links render. So Connect
Wallet only works once this is hosted as its own site.

## Run it locally first (optional but recommended)

```bash
npm install
npm run dev
```

Open the printed `http://localhost:5173` URL. On desktop with the MetaMask
extension installed, Connect Wallet should work immediately — localhost is
one of the origins MetaMask always trusts.

## Deploy — pick one

### Option A: Vercel (fastest)

```bash
npm install -g vercel
vercel
```

Follow the prompts (accept the defaults — Vercel auto-detects Vite). You'll
get a `https://your-project.vercel.app` URL. Open that URL inside MetaMask
mobile's built-in browser (or any desktop browser with the extension) and
Connect Wallet will work.

### Option B: Netlify

```bash
npm install
npm run build
npx netlify-cli deploy --prod --dir=dist
```

Or: push this folder to a GitHub repo, then in the Netlify dashboard choose
"Import from Git" — it will pick up `netlify.toml` automatically (build
command `npm run build`, publish directory `dist`).

### Option C: GitHub Pages

```bash
npm install
npm run build
```

Then push the contents of `dist/` to a `gh-pages` branch (or use the
`gh-pages` npm package: `npm install -D gh-pages`, add
`"deploy": "gh-pages -d dist"` to package.json scripts, then
`npm run deploy`). Enable Pages for that branch in your repo settings.

## After deploying

Open the live URL inside MetaMask mobile's browser (or a desktop browser
with the extension installed and unlocked) — not a Claude artifact link.
Tap **Connect Wallet**; you should see your address, network name, and ETH
balance appear in the header.

## Project structure

```
├── index.html       entry HTML
├── src/
│   ├── main.jsx      mounts <App /> into #root
│   └── App.jsx       the full ArbScan dashboard (your uploaded component)
├── package.json
├── vite.config.js
└── netlify.toml      build settings for Netlify
```
