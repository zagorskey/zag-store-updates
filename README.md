# Zag Store Updates

Official distribution metadata for **Zag Store**.

- Development: [zagorskey/zag-store](https://github.com/zagorskey/zag-store)
- Website: https://zagstore.app
- Channels: Stable, Beta, Nightly
- Initial release target: **1.0.0 Beta (Build 1)**, not yet published

## Release state

**No releases are published.** All channel feeds currently contain `release: null`. No feed should be interpreted as an installation instruction.

## Security model

The channel JSON files are **unsigned bootstrap placeholders**, not trusted update metadata. Clients MUST NOT automatically download or install applications based on these files. Before enabling client-side update discovery, implement and test authenticated update metadata using an established framework (preferably TUF), including trusted root/key distribution, expiration, anti-rollback, and recovery. Independently verify IPA integrity, bundle identifier, signing identity, entitlements and compatibility.

Never publish private signing keys, certificates with private keys, credentials, user backups or developer diagnostics here.

## Distribution

Release assets will be hosted as immutable GitHub Release assets, not committed to Git history. A validated publication must include the signed IPA, integrity metadata, release notes and GPLv3 corresponding source. Promotion between channels should reuse the same verified artifact.

See [release policy](docs/release-policy.md) and [security policy](docs/security.md).
