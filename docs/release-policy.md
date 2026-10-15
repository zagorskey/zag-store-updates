# Release policy

## Channels

- **Stable**: validated general release.
- **Beta**: opt-in pre-release, initially targeting 1.0.0 (Build 1).
- **Nightly**: opt-in development snapshots; may be less reliable.

All channels are currently empty. A channel must never point to a nonexistent or unverified IPA.

## Release gates

1. Record source commit and reproducible build inputs.
2. Build a release candidate without changing the installed app.
3. Verify IPA structure, version, bundle ID (`app.zagstore.ios`), entitlements and signing identity after signing.
4. Record SHA-256, file size, release notes and source archive.
5. Verify corresponding GPLv3 source availability, including modifications and build/install instructions.
6. Publish immutable versioned release assets; never silently replace a published asset.
7. Publish authenticated metadata only after all assets are available and validated.
8. Verify discovery, download and native installation on a test installation before enabling automatic updates.

**Migration:** An existing installation with bundle ID `com.cwd43.gu29` is a separate iOS app. A new `app.zagstore.ios` install will not be an in-place update of it. The source's new Build 1 must not be offered as an update to the old identity.

Release tags should distinguish channels, e.g. `v1.0.0-beta.1`. The actual Info.plist version and build are checked independently. No release workflow should rewrite build numbers from Git commit hashes.

## Automation

Publishing must be manual and gated initially. Do not enable the inherited Feather release workflows until replaced and validated.

## Sensitive embedded material gate

Prior to accepting any IPA, inspect all packaged resources for embedded private keys and credentials. The development Makefile currently copies `deps/*` into the app after applying an ad-hoc signature. A PEM extension is not proof of private-key content; inspect file types without printing secrets. If private keys are embedded, stop release publication, remove them from the distribution build, and rotate exposed credentials if warranted. Changes to bundle contents after signing require re-signing and re-verification. Never publish a CI build as installable merely because `codesign --sign -` succeeded.
