# Aether — Cloud Expert

Animated frontend prototype for **Aether**, a cloud storage service. It is plain HTML, CSS and JavaScript with no build step and no framework, so it runs anywhere, including GitHub Pages.

## Features

- **Cinematic intro.** Particles gather into a glowing halo while the logo wipes in and the tagline types itself out. Click or press *Skip intro* to jump straight in.
- **Sign in / create account (Page A).** Floating-label forms with animated validation (shake, inline errors, success ticks) and a **Test Admin Login** button that skips auth.
- **Dashboard (Page B).** Animated stat counters, a storage capacity ring, a breakdown by file type, recent files and recent billing.
- **Storage manager.** Drag-and-drop or click-to-upload with animated progress, demo-file generator, search, type filters, grid/list views, and download and delete actions.
- **Test tier.** A toggle in the sidebar (or the avatar menu on mobile) gives unlimited free storage, so you never hit the paywall while testing.
- **Transactions.** Billing history with status filters (Paid / Pending / Failed / Refunded), search and invoice download.
- **Pricing & checkout (Page C).** Monthly/yearly sliding toggle with animated price changes, five plans, and a checkout modal (Card or UPI) with input masks, validation, a simulated decline and a success animation.
- **Why we're the cheapest.** Animated cost-per-GB comparison cards, six cost-efficiency pillars and a per-plan price-per-GB chart.
- Responsive down to phone width (bottom tab bar on mobile) and respects `prefers-reduced-motion`.

## Plans

| Plan | Storage | Monthly | Yearly |
|---|---|---|---|
| Starter | 5 GB | Rs. 45 | Rs. 450 |
| Creator | 50 GB | Rs. 260 | Rs. 2,600 |
| Pro | 100 GB | Rs. 440 | Rs. 4,400 |
| Team | 200 GB | Rs. 850 | Rs. 8,500 |
| Business | 500 GB | Rs. 2,100 | Rs. 21,000 |

Plan names, features and prices live in `js/config.js`.

## Project structure

```
aether-cloud/
├── index.html              # App shell, intro overlay, script includes
├── css/
│   └── styles.css          # Design tokens, components, animations, responsive rules
├── js/
│   ├── config.js           # Plans, prices, API endpoints, test admin account
│   ├── services.js         # ★ Backend hook points: auth, storage, payments, billing
│   ├── store.js            # App state (persisted to localStorage) and demo seed data
│   ├── ui.js               # Icons, formatting, kinetic text, reveals, toasts, modals, validation
│   ├── app.js              # Hash router, sidebar/topbar, cinematic intro
│   └── views/
│       ├── auth.js         # Page A: sign in / sign up
│       ├── dashboard.js    # Page B: overview
│       ├── files.js        # Page B: storage file manager
│       ├── transactions.js # Page B: billing history
│       ├── pricing.js      # Page C: pricing + checkout modal
│       └── why.js          # "Why we are the cheapest"
└── assets/
    ├── aether-logo.png     # Full logo (transparent background)
    └── aether-icon.png     # Icon mark / favicon
```

## Run locally

Open `index.html` in a browser. To serve it instead:

```bash
npx serve .
```

or

```bash
python -m http.server 8080
```

## Deploy to GitHub Pages

1. Push this folder to a GitHub repository.
2. Go to **Settings → Pages**, set *Source* to **Deploy from a branch**, then pick `main` and `/ (root)`.
3. The site is published at `https://<your-username>.github.io/<repo-name>/`.

## Connecting a real backend

Every network call goes through `js/services.js`. Look for these comments:

- `// ── Connect auth backend here` for login, signup, logout and password reset
- `// ── Connect storage backend here` for list, upload (with progress), download and delete
- `// ── Connect payment gateway here` for checkout (Razorpay, Stripe, PayHere, etc.)
- `// ── Connect billing database here` for invoices and transactions

Each mock function already returns the shape the UI expects. Replace the body with a `fetch` call and keep the return value the same. Put your endpoints in `Aether.config.api` in `js/config.js`.

> **Security note:** don't collect raw card numbers in your own form in production. Use your gateway's hosted fields or SDK. The checkout form here is for demonstration only.

## Testing tips

- **Test Admin Login** signs you in with demo files, invoices and the unlimited test tier switched on.
- Turn the **Test tier** off to see the plan limits and paywall in action.
- Create a normal account to get the new-user flow, which lands on Pricing.
- At checkout, any test details work. A card number ending in **0002** simulates a declined payment.
- To start over, sign out. This clears the prototype data stored in your browser.

## Notes

The competitor figures on the *Why Us* page are illustrative placeholders. Replace them with verified market data before launch.
