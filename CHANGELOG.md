# Changelog

All notable changes to the WARB desktop app are documented here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project
adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Each released version below corresponds to a
[GitHub Release](https://github.com/AnasShwehdy/warb-releases/releases) with signed installers
attached. warb.network renders these notes directly from that API.

## [Unreleased]

## [0.1.0-beta.1] - 2026-07-30

First public devnet build.

### Added

- **Capacity order book.** Listings are Solana accounts discovered with `getProgramAccounts` —
  there is no WARB API and no index. Filter live capacity by provider, model and price per Mtok.
- **Wrap/unwrap helpers for the wSOL escrow mint**, so funding and closing a session doesn't
  require a separate SPL-token tool.
- **Buyer-funded sessions.** Opening a session escrows wSOL in a program-derived vault sized to the
  tokens purchased and commits the buyer's hash anchor on chain.
- **PayWord settlement.** The buyer generates the hash chain and releases one preimage per tick of
  delivered work; the seller settles the whole session in a single `claim_ticks` transaction.
  Spend is bounded independently in three places — the buyer's authoriser, the seller's credit
  window, and the program's `tokens_purchased` cap.
- **End-to-end encrypted transport.** X25519 + HKDF + ChaCha20-Poly1305 between buyer and seller.
  Both public keys are published on chain, so the relay has no key exchange to intercept.
- **Blind mesh relay.** The gateway routes opaque `SealedFrame` ciphertext and holds no authority
  over capacity, price or settlement. Brief reconnect buffering keeps a streaming response alive
  across a dropped socket.
- **Failover as an offer, never a silent reroute.** On seller drop the relay names candidates; the
  buyer's client verifies price and capacity on chain and signs a new session.
- **Provider-agnostic seller onboarding.** Adapters for `claude-cli`, `cursor`, `antigravity` and
  `openai` detect a local install, report auth state without touching credentials, and normalise
  quota into a common shape. New providers are new adapter modules only.
- **Embedded wallet.** BIP39 → SLIP-0010 derivation on Solana path `m/44'/501'/0'/0'`, balance and
  SPL-token indexing, devnet airdrop, and native SOL transfers.
- **Seller-side privacy.** Decrypted prompts stay in Rust and are never passed to the webview or
  written to disk; no transcript of buyer work is retained on the seller.
- **Sandboxed agent runtime.** File I/O is chrooted to `./current_workspace` and terminal commands
  pass a RegEx allowlist with an overriding denylist.

### Known limitations

- **Beta.** Devnet only. The program is **not audited** — do not route production secrets or real
  value. Wire formats and on-chain layouts may still change between beta builds.
- Seller capacity is self-reported by the provider adapter and not independently attested.

[Unreleased]: https://github.com/AnasShwehdy/warb-releases/compare/v0.1.0-beta.1...HEAD
[0.1.0-beta.1]: https://github.com/AnasShwehdy/warb-releases/releases/tag/v0.1.0-beta.1
