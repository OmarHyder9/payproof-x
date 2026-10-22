# X Layer TapeOut Accelerate — submission notes

## Project

**PayProof X — Shareable stablecoin invoices and on-chain payment verification**

## Short pitch

PayProof X helps freelancers, small online sellers, and service operators issue clear USDT/USDC invoices and verify payments without trusting screenshots or sender messages. It reads X Layer transaction receipts and checks the expected token contract, recipient, transferred amount, and block confirmations. The static app does not custody funds or request private keys.

## Target users and acquisition

- Freelancers paid directly in stablecoins.
- Small online services and creators issuing one-off invoices.
- Developers who need a small payment-verification component before offering a full checkout backend.

Initial acquisition: developer communities, freelance communities that allow crypto payments, open-source distribution, and direct outreach to small merchants who already accept X Layer assets.

## Proposed revenue model

Keep the basic static verifier free. Charge for paid implementation work: branded deployments, custom integrations for a merchant site or bot, and setup/support. Offer a fixed scope and quote for each deployment; collect agreed fees in USDT or USDC on a clearly agreed network. A future hosted subscription would require a backend for account management, entitlement checks, payment reconciliation, and refunds; that is not implemented in this static version.

## X Layer usage implemented

The app queries X Layer's public JSON-RPC endpoint, checks chain ID `196`, reads `eth_getTransactionReceipt` and `eth_blockNumber`, and validates ERC-20 `Transfer` logs for the configured token contract and recipient. Relevant official references:

- <https://web3.okx.com/onchainos/dev-docs/xlayer/developer/rpc-endpoints/rpc-endpoints>
- <https://web3.okx.com/ar/onchainos/dev-docs/xlayer/developer/build-on-xlayer/contracts>
- <https://web3.okx.com/sv/learn/usdc-cctp-on-xlayer>

No custom TapeOut circuit or contract is deployed in this version. The public event page asks projects to explain the TapeOut ecosystem features they use. Before entering, check the current official wording and add/document a direct TapeOut ecosystem integration if required or if it would make the submission stronger. Do not claim a TapeOut contract/circuit is used when it is not.

## Demo path

1. Open the app and enter a recipient address, token, and amount.
2. Create and share the generated invoice URL.
3. Paste a real X Layer transaction hash into the verification panel.
4. Show the token contract, matching transfer, recipient, amount, confirmations, and JSON receipt download.

Use a real public transaction or a test transaction only where suitable. Never expose a private key or recovery phrase in a demo.

## Risks and limitations

- Public RPC endpoints may rate-limit requests or change service behavior.
- The app verifies receipt logs, not the commercial identity of a payer.
- The QR generator currently sends the public invoice URL to a third-party QR service.
- Public GitHub Pages serves static files only; a hosted subscription is not implemented here.
- Prize participation is subject to current event terms, eligibility and compliance checks, and the submission deadline. No prize or customer revenue is guaranteed.
