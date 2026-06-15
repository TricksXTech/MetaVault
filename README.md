# 🤝 Contributing to MetaVault — Chains & Tokens Registry

> MetaVault is an open-source multi-chain crypto wallet. We welcome community contributions to expand our supported networks and token lists — but to keep our users safe, **all submissions go through a review process**.

---

## 📋 Table of Contents

- [What You Can Contribute](#what-you-can-contribute)
- [Requirements Before Submitting](#requirements-before-submitting)
- [How to Add a Chain](#how-to-add-a-chain)
- [How to Add a Token](#how-to-add-a-token)
- [File Formats](#file-formats)
- [Audit Requirement](#audit-requirement)
- [Submission Process](#submission-process)
- [Review Criteria](#review-criteria)
- [Rejection Policy](#rejection-policy)
- [FAQ](#faq)

---

## What You Can Contribute

We accept community pull requests for:

| Type | File | Description |
|---|---|---|
| 🔗 New Chain | `chains.json` | Add support for a new EVM-compatible network |
| 🪙 New Token | `tokens.json` | List a verified token on an existing supported chain |
| 🖼️ Logo | `logos/chains/` or `logos/tokens/` | Add or update chain/token logo images |

We do **not** accept:
- Edits to wallet core logic, security modules, or smart contracts via data PRs
- Unverified, scam, or rug-pulled tokens
- Testnets (unless explicitly requested by the team)
- Tokens without a publicly accessible audit

---

## Requirements Before Submitting

Before opening a pull request, make sure your project meets **all** of the following:

### ✅ For Tokens

- [ ] **Smart contract is publicly deployed** on a mainnet chain already listed in `chains.json`
- [ ] **Token contract is verified** on the chain's block explorer (e.g. Etherscan, BscScan)
- [ ] **Audit report is publicly available** from a recognized security firm (see [Audit Requirement](#audit-requirement))
- [ ] **Logo is provided** in PNG format, 256×256px, transparent background
- [ ] **Price source is specified** (CoinGecko, DexScreener, or similar)
- [ ] Token is **not blacklisted** or associated with any known exploit or fraud

### ✅ For Chains

- [ ] EVM-compatible (chain ID, RPC endpoint, standard decimals)
- [ ] Publicly accessible RPC with reasonable uptime
- [ ] Active block explorer available
- [ ] Chain is live on mainnet (not a testnet)
- [ ] Logo provided in PNG format, 256×256px, transparent background
- [ ] Listed on CoinGecko with a valid `coingecko_id`

---

## How to Add a Chain

Add an entry to `chains.json` following this exact structure:

```json
{
  "id": "your_chain_id",
  "name": "Your Chain Name",
  "symbol": "SYMBOL",
  "chain_id": 12345,
  "rpc": "https://your-chain-rpc.example.com",
  "explorer": "https://your-explorer.example.com",
  "decimals": 18,
  "logo": "https://raw.githubusercontent.com/TricksXTech/MetaVault/main/logos/chains/yourchain.png",
  "coingecko_id": "your-coingecko-id",
  "is_testnet": false,
  "enabled": true
}
```

> ⚠️ The `id` field must be lowercase, unique, and use underscores (no spaces or hyphens).

---

## How to Add a Token

Add an entry to `tokens.json` following this exact structure:

```json
{
  "chain": "bnb",
  "contract": "0xYourContractAddress",
  "name": "Your Token Name",
  "symbol": "TKN",
  "decimals": 18,
  "logo": "https://raw.githubusercontent.com/TricksXTech/MetaVault/main/logos/tokens/tkn.png",
  "verified": true,
  "price_sources": [
    {
      "type": "coingecko",
      "id": "your-coingecko-id"
    }
  ]
}
```

**Supported `price_sources` types:**

| Type | Required Field | Example |
|---|---|---|
| `coingecko` | `id` | `"id": "tether"` |
| `dexscreener` | `pair` | `"pair": "0xPairAddress"` |

---

## File Formats

### Logo Guidelines

| Property | Requirement |
|---|---|
| Format | `.png` only |
| Size | 256 × 256 pixels |
| Background | Transparent |
| File name | Lowercase symbol, e.g. `usdt.png`, `eth.png` |
| Location | `logos/tokens/` for tokens, `logos/chains/` for chains |

Do **not** submit JPG, SVG, or WebP logos. They will be rejected automatically.

---

## Audit Requirement

**This is mandatory. We will not merge token listings without a publicly accessible audit report.**

### Accepted Audit Firms

We recognize audits from (but not limited to):

- [CertiK](https://www.certik.com/)
- [PeckShield](https://peckshield.com/)
- [Hacken](https://hacken.io/)
- [SlowMist](https://www.slowmist.com/)
- [Trail of Bits](https://www.trailofbits.com/)
- [OpenZeppelin](https://www.openzeppelin.com/)
- [Quantstamp](https://quantstamp.com/)
- [Solidproof](https://solidproof.io/)

### What to Include

In your pull request, you must provide:

1. **A direct link to the full audit report** (PDF or public URL)
2. **The auditing firm's name**
3. **Audit date** (must be within the last 2 years)
4. **Audit scope** — confirm the specific contract address being listed was included in the audit

> ⚠️ Self-audits, GitHub security reviews, or automated scanner results (e.g. GoPlus, TokenSniffer alone) are **not** accepted as audits.

---

## Submission Process

1. **Fork** this repository
2. **Create a new branch** named `add/chain-<name>` or `add/token-<symbol>-<chain>`
3. **Add your entry** to the appropriate JSON file
4. **Add your logo** to the correct folder
5. **Open a Pull Request** against the `main` branch using our PR template
6. **Fill in all required fields** in the PR description, including the audit link
7. **Wait for review** — our team aims to respond within 5–7 business days

### PR Title Format

```
[Chain] Add <Chain Name>
[Token] Add <TOKEN_SYMBOL> on <Chain Name>
```

**Examples:**
```
[Token] Add USDT on Arbitrum
[Chain] Add ZetaChain
```

---

## Review Criteria

Our team evaluates every submission against the following:

| Criteria | Details |
|---|---|
| 🔐 Security | Valid audit from a recognized firm, no known exploits |
| ✅ Accuracy | Contract address verified on-chain, correct decimals and symbol |
| 🖼️ Quality | Logo meets spec (256×256 PNG, transparent) |
| 📊 Activity | Project shows signs of active development and legitimate usage |
| 💬 Transparency | Team is identifiable; social/community presence exists |
| ⚖️ Compliance | Project does not violate applicable laws or our terms |

---

## Rejection Policy

Your PR may be closed without merging if:

- The audit link is missing, expired, or from an unrecognized source
- The contract is unverified on the block explorer
- The token or chain has been flagged for fraud, exploit, or rug pull
- Logo specs are not met
- Required PR fields are left blank
- A duplicate entry already exists

Rejected PRs can be re-submitted after addressing the issues. Open an issue first if you're unsure.

---

## FAQ

**Q: My token doesn't have a CoinGecko listing. Can I still submit?**
Yes. Use `dexscreener` as the price source with the pair contract address. However, your token still needs a valid audit.

**Q: Can I add a testnet chain?**
Not via community PR. Testnet additions are handled internally by the MetaVault team.

**Q: How long does review take?**
We aim for 5–7 business days. Complex submissions or those requiring additional verification may take longer.

**Q: Can I submit multiple tokens in one PR?**
You may submit up to 3 tokens per PR if they share the same chain and project. For large batches, open an issue first to discuss.

**Q: What if my audit is older than 2 years?**
Older audits may still be considered if the contract is unchanged and the project has no known vulnerabilities. Include a note in your PR explaining the situation.

**Q: Who decides what gets listed?**
The MetaVault core team has final say on all listings. This is not a decentralized registry — we maintain editorial control to protect our users.

---

## 📬 Questions?

Open an [issue](../../issues) or reach out to us via our community channels.

---

> MetaVault is committed to keeping our users safe. We appreciate every contribution — but user protection always comes first.
