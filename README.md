# PayProof X

**A bilingual (Arabic/English), non-custodial stablecoin invoice and on-chain payment verification tool for X Layer mainnet.**

PayProof X creates shareable invoice links for **USDT** and **native Circle-issued USDC** on X Layer (chain ID `196`). A recipient can verify a transaction by checking the ERC-20 `Transfer` logs in the transaction receipt using the public X Layer JSON-RPC endpoint.

## Features

- Arabic RTL and English LTR interface.
- Invoice links with recipient, token, amount, optional reference and due date.
- QR code for the shareable invoice link.
- Read-only transaction verification: X Layer chain ID, successful receipt, supported token contract, recipient, received amount and confirmation count.
- Downloadable JSON verification record.
- No wallet connection, private keys, seed phrases, account system, or server-side custody.
- Static deployment; no build step or package installation required.

## Supported network and token contracts

- X Layer mainnet — chain ID `196`
- RPC: `https://rpc.xlayer.tech`
- USDT: `0x1E4a5963aBFD975d8c9021ce480b42188849D41d`
- Native USDC: `0xB6CEceAB302E2E4948951eE7843FC24E92933061`

**Token note:** This version supports native USDC only; legacy bridged USDC contracts are intentionally not treated as equivalent. Confirm token contract addresses against official documentation before any production payment decisions.

## Run locally

Open `index.html` in a current desktop or mobile browser. Internet access is required for blockchain verification and QR generation. Some browsers restrict network calls from `file://` pages; in that case run a local static server, for example:

```bash
python -m http.server 8080
```

Then open `http://localhost:8080` from this directory.

## Deploy on GitHub Pages

The current repository is published as a static site. Recent GitHub Pages deployment runs succeeded, but the `.github/workflows/pages.yml` file is not present on the `main` branch. These instructions therefore describe branch-based deployment rather than a workflow that is not currently in the branch.

1. Open **Settings → Pages** in this repository.
2. Under **Build and deployment → Source**, select **Deploy from a branch**.
3. Select branch `main` and folder `/(root)`, then save.
4. Wait for the Pages deployment to complete and use the published URL shown in the Pages settings.

If you later switch the Pages source to **GitHub Actions**, first add and review a dedicated workflow under `.github/workflows/` and verify that it completes successfully. Do not assume a workflow exists unless the file is present on the branch.

## Security and correctness notes

- This application never asks for or handles private keys and cannot move funds.
- Verification relies on a public RPC endpoint. Public RPCs can rate-limit, return temporary errors, or change policies; verify important payments independently in a trusted block explorer as well.
- A transaction is marked verified only if its receipt succeeded, a supported token contract emitted a `Transfer` log to the specified recipient with an aggregate value at least equal to the requested amount, and the selected confirmation count has been reached.
- This is a payment-evidence utility, not a substitute for an independent security review, accounting controls, or confirming the actual token contract and commercial terms.
- QR generation currently sends the public invoice URL to `api.qrserver.com`. The URL includes the wallet address and invoice details. Do not put secret data into invoice references. If you do not want that third-party request, replace the QR generation service with a self-hosted QR library.
- No analytics, cookies, login, database, or server component is included.

## Business model (not embedded or guaranteed)

The static app is a free utility, not a subscription SaaS. Potential revenue paths include hosted branded instances, paid integrations for merchants/bots, and custom deployment/support paid in USDT or USDC. A reliable recurring subscription would require an additional backend for identity, entitlements, refunds and payment reconciliation; do not represent a client-side-only feature flag as secure payment enforcement.

## Sources

- X Layer RPC endpoints: <https://web3.okx.com/onchainos/dev-docs/xlayer/developer/rpc-endpoints/rpc-endpoints>
- X Layer contract addresses: <https://web3.okx.com/ar/onchainos/dev-docs/xlayer/developer/build-on-xlayer/contracts>
- Native USDC on X Layer: <https://web3.okx.com/sv/learn/usdc-cctp-on-xlayer>

## License

MIT — see `LICENSE`.
