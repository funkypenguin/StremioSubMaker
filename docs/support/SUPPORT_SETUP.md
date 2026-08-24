# SubMaker support page setup

The support page is a static, GitHub Pages-ready site in this folder. Its public URL will be:

`https://xtremexq.github.io/StremioSubMaker/support/`

The page deliberately says **Support SubMaker**, not “Donate” or “Buy me a coffee.” “Support” fits an open-source project, keeps the focus on maintenance, and does not suggest that SubMaker is a charity. A coffee metaphor can still work in a Reddit post or button caption, but it should not be the main framing.

## Recommended payment mix

Use three clear choices:

1. **GitHub Sponsors** — the default for recurring and one-time support. The live profile is `https://github.com/sponsors/xtremexq`. GitHub currently charges no fee for sponsorships from personal accounts.
2. **PayPal payment link** — the one-time fallback for non-GitHub users. The current PayPal account is personal; PayPal requires a Business account before it will create a reusable payment link. Keep this method disabled until that account decision and setup are complete.
3. **NOWPayments donation link** — one hosted crypto checkout instead of publishing separate wallet addresses. It supports BTC, XMR, and hundreds of other assets. Standard same-coin processing is 0.5%; conversion is 1% total; custody withdrawals have no service fee, only the relevant network fee. Custody is useful for batching withdrawals so small contributions do not each trigger an outbound network fee.

For settlement, use a private wallet when preserving the received asset matters. To settle to an exchange, configure an asset and network that the exchange currently supports, or auto-convert to a supported stablecoin first. Never send an asset to an exchange address unless both the coin and network match exactly.

Current official references:

- [GitHub Sponsors availability and fees](https://docs.github.com/en/sponsors/getting-started-with-github-sponsors/about-github-sponsors)
- [PayPal buttons and payment links](https://www.paypal.com/br/business/accept-payments/payment-links)
- [NOWPayments pricing](https://nowpayments.io/pricing)
- [NOWPayments supported coins](https://nowpayments.io/supported-coins)
- [NOWPayments donation tools](https://nowpayments.io/donation-tools)

Provider rules and prices change, so check those pages again before launch.

## 1. Add payment details

Edit [`support-data.json`](support-data.json). Each method stays visibly in “Setup” mode until both conditions are true:

- `enabled` is `true`;
- its URL/address no longer contains a placeholder such as `YOUR_` or `REPLACE_`.

Example:

```json
{
  "id": "paypal",
  "label": "PayPal",
  "shortLabel": "PayPal",
  "description": "Quick one-time support",
  "badge": "",
  "enabled": true,
  "url": "https://www.paypal.com/ncp/payment/actual-link-id",
  "amountMode": "provider"
}
```

For crypto, create a NOWPayments account, enable 2FA, open **Payment Tools → Donations**, create a link such as `nowpayments.io/donation/submaker`, and paste it into the `crypto` method's `url`. Set `enabled` to `true` only after a small test payment and withdrawal.

GitHub Sponsors is already connected. Create one-time tiers at `$3`, `$5`, `$10`, and `$25` and a small set of monthly tiers if you want stronger amount anchoring. Keep tier benefits simple: public thanks if requested and occasional project updates. Do not promise priority support or delivery dates.

## 2. Set up public recognition

GitHub Pages cannot receive or store form submissions. Use a private Google Form, Tally form, or similar free hosted form, then place its HTTPS URL in `settings.recognitionFormUrl`. Set `settings.recognitionUsernameParameter` to the form's username query parameter so the username entered on the support page is carried into the form. For a prefilled Google Form this is usually an `entry.NUMBER` parameter; other providers may accept a named parameter such as `username`.

Suggested fields:

- Payment method
- Approximate payment date
- Public nickname/handle — prefilled from the support page when the form provider supports it
- “Show my amount publicly?” — unchecked by default
- Optional private email or short payment-reference suffix for verification

Never request or publish a complete transaction ID, legal name, email address, wallet address, or payment screenshot. Keep the form private. The username field on the support page records no data by itself; after checkout, the supporter must open and submit the configured recognition form. Anonymous supporters do nothing.

## 3. Add public supporters

Only add someone after receiving explicit opt-in through the recognition form:

```json
{
  "name": "subtitle-fan",
  "public": true,
  "since": "Sep 2026",
  "note": "Early supporter"
}
```

Do not infer consent from a public payment-provider username. GitHub Sponsors also lets sponsors make their sponsorship private; respect that setting.

Update `settings.anonymousSupportCount` manually to credit anonymous supporters without identifying them.

## 4. Publish for free with GitHub Pages

1. Push the files to the default `main` branch.
2. Open the repository’s **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select `main` and `/docs`, then save.
5. Wait for the Pages workflow to complete and open `https://xtremexq.github.io/StremioSubMaker/support/`.

GitHub Pages is free for this public repository. It hosts the page, CSS, JavaScript, and public supporter list. It does **not** process money, keep secrets, run server code, or receive form data.

The repository also includes `.github/FUNDING.yml`, which connects GitHub’s Sponsor button to both the active Sponsors profile and this support hub:

```yaml
github: xtremexq
custom: "https://xtremexq.github.io/StremioSubMaker/support/"
```

## 5. Launch checklist

- Complete payment-provider identity, tax, payout, and account-security setup.
- Replace every placeholder and enable only tested methods.
- Make a small test transaction through each enabled method.
- Test the recognition form without publishing any private response fields.
- Enable GitHub Pages and test on both mobile and desktop.
- Post the short explanation below instead of a long personal appeal.

Suggested announcement copy:

> SubMaker is free and its public hosting is generously sponsored by ElfHosted. A few people asked for a way to help with the parts hosting does not cover: AI/API credits, RD/TB test access, maintenance tools, and the time behind fixes. I’ve added an optional support page with one-time, recurring, and privacy-friendly choices. Using the project and reporting good bugs still helps plenty.

Suggested CTA: **Help keep SubMaker in sync →**
