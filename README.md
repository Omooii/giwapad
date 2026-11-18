# GiwaPad — Token Launchpad on GIWA Sepolia

GiwaPad is a **testnet** token launchpad built with the Ammora SDK
(`@ammora-protocol/sdk@0.3.9`) on **GIWA Sepolia (chain 91342)**. It was built for
the Ammora Season 2 **Builder mission**: an exchange/launchpad built with the
Ammora SDK.

**Live site:** https://omooii.github.io/giwapad/

> Testnet only. Tokens launched here have no value. Never send real funds.

## What it does

- **Connect wallet** — injected wallet (MetaMask / Bitget Wallet), auto-switches to
  GIWA Sepolia (chain 91342).
- **Launch a token** — creates a new token + its pre-graduation Ammora bonding
  curve (ALC) in one transaction, on the GiwaPad platform Config **#56**.
  The caller becomes the token's Creator. Launching is free of protocol fees
  (gas only) on this Config.
- **Trade** — buy with WETH / sell tokens on the bonding curve, with live SDK
  quotes, slippage protection (0.5%), exact-amount approvals, and simulation
  before signing.
- **Graduation progress** — live curve status (Active / Ready to migrate /
  Migrated), quote raised vs. the 0.01 WETH graduation threshold, and the
  graduated pool address after migration.
- **Wrap ETH → WETH** — buys need WETH; wrap testnet ETH in one click.
- **Launches** — featured launch plus tokens you launched from the browser
  (kept in local storage).

The app verifies the Ammora V4 core contracts on load
(`verifyAmmoraV4CoreAtBlock`) and authenticates every curve against the
reviewed LaunchFactory + fee policy before displaying it.

## Verified on-chain (GIWA Sepolia)

All smoke-test transactions were executed with the launchpad's testnet wallet
`0x0f9C24dF885e525586dC3290255847F16a467adA`:

| Step | Transaction |
| --- | --- |
| Config #56 created (template #6, 1M-token sale supply, 0.01 WETH threshold) | [0xef2d8615…](https://sepolia-explorer.giwa.io/tx/0xef2d861588b35a5f49d33223e1e38f471e84f5463031d0e9064f286986f3b8b4) |
| Test token GPTEST launched | [0xf3529224…](https://sepolia-explorer.giwa.io/tx/0xf3529224fc2216c5380c60e8484faf77c3651ed00aa4381214d2534e2a33e042) |
| Wrapped 0.002 ETH → WETH | [0x41e41a56…](https://sepolia-explorer.giwa.io/tx/0x41e41a568a48e694fbeb7426f8fe8691bfd368a540c936e905481a147bdb93a9) |
| Buy: 0.0005 WETH → 963,016 GPTEST | [0xdd61801e…](https://sepolia-explorer.giwa.io/tx/0xdd61801ed7188a45d6b4ba796ef904674e2c6b3092a3adda14b4ec79bfdcead9) |
| Sell: 100,000 GPTEST → 0.000367 WETH | [0xc78dca41…](https://sepolia-explorer.giwa.io/tx/0xc78dca4138d1c5356ccac0cdc50a5339f8d278f8019aaaa5064e92aa705b8e9b) |

- Test token: `0x81Dc4e60C7567F214A216ab6Ce1182D0c482a939` (GPTEST, 9 decimals)
- Test curve: `0x74b114a001dDe7926d81991Ae7e2369551B60FAd`
- Config #56 hash: `0xe072f2e2152cb583f79b3b79877445d8a345f8eda338e32bcaf843eb06743090`

## Development

The source lives in `app/src/main.js` (ESM, SDK + viem). Build the bundle with:

```bash
cd app
npm install
npx esbuild src/main.js --bundle --format=iife --platform=browser --target=es2020 --minify --outfile=public/app.js
```

Then serve `public/` (or copy it to the repo root for GitHub Pages).

The `ammora-examples/` directory in the workspace holds the reviewed Ammora
example project (SDK 0.3.9) used as the reference for the Config / launch /
trade flows and for the smoke tests above.

## Links

- Ammora launchpad guide: https://docs.ammora.org/guides/launchpad
- Ammora SDK docs: https://ammora-docs.vercel.app
- GIWA Sepolia explorer: https://sepolia-explorer.giwa.io
- Ammora Season 2: https://ammora.org
