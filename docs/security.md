# Update security policy

## Current state

This repository contains only **unauthenticated, empty channel placeholders**. There are no trusted metadata keys, signed releases, update endpoints or automatic update capability yet. The feeds are intentionally **not safe to use for installation**.

## Planned authenticated metadata

Adopt an established framework such as [The Update Framework (TUF)](https://theupdateframework.io/) instead of inventing a signature format. Design and test trusted root/key provisioning, threshold signatures where appropriate, expiration, key rotation, snapshot consistency and rollback/freeze protection. Keep private keys out of GitHub and CI logs.

Client verification must include:
- authenticated metadata and anti-rollback checks;
- exact asset digest and size;
- expected bundle identifier `app.zagstore.ios`;
- signing identity and entitlement policy verification;
- version/build/channel compatibility and explicit user confirmation for manual updates.

HTTPS and SHA-256 alone do not authenticate a maliciously replaced manifest. Metadata signatures do not replace IPA signing verification.

## Reporting

Until a dedicated security contact is published, avoid posting vulnerabilities or private keys in public issues.
