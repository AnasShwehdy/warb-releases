# WARB — releases

Public distribution for the [WARB](https://warb.network) desktop app.

**This repository contains no source code.** It holds the signed installers, their checksums, and
the changelog. The protocol, wallet, relay and Anchor program live in a private repository.

## Download

Always-current links, resolved by warb.network:

| Platform | Link |
| --- | --- |
| macOS · Apple Silicon | <https://warb.network/download/latest/darwin/arm64> |
| macOS · Intel | <https://warb.network/download/latest/darwin/x64> |
| Windows · x64 | <https://warb.network/download/latest/windows/x64> |
| Linux · x64 | <https://warb.network/download/latest/linux/x64> *(not yet shipping)* |

Or pick a specific build from [Releases](https://github.com/AnasShwehdy/warb-releases/releases).

## Verifying a download

Every release ships a `SHA256SUMS.txt` listing each artifact.

```bash
# macOS / Linux
shasum -a 256 -c SHA256SUMS.txt --ignore-missing
```

```powershell
# Windows
Get-FileHash .\WARB_0.1.0_x64-setup.exe -Algorithm SHA256
```

## Versioning

[Semantic versioning](https://semver.org). Tags are `vMAJOR.MINOR.PATCH`, and the tag is the single
source of truth — `warb.network` reads this repo's Releases API at request time, so publishing a
release is what makes a version appear on the site. See [CHANGELOG.md](CHANGELOG.md).

While WARB is on Solana **devnet**, treat every build as a beta: the on-chain program is unaudited
and devnet state is periodically reset.

## Reporting a problem

Open an issue here for anything about a *build* — install failures, crashes on launch, a corrupt
artifact, a wrong checksum. Protocol and security reports should go to the address in the release
notes rather than a public issue.
