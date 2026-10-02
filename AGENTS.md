# Shopwell repository rules

This repository is the independently maintained Shopwell fork of the STS Action.

- Preserve UTF-8 and existing user changes.
- Project-owned files use Apache License 2.0; root `LICENSE` is the standard text.
- Preserve the upstream license verbatim in root `NOTICE`; do not reintroduce Shopware branding outside legal text.
- Do not merge or cherry-pick upstream history, copy upstream tags, or force-push.
- Before reporting a successful sync, run `./bin/syncctl audit-license octo-sts-action`,
  `./bin/syncctl audit-repository-identity octo-sts-action`,
  `./bin/syncctl audit-dependency-parity octo-sts-action`, and
  `./bin/syncctl audit-upstream-dependencies octo-sts-action` from `/Users/goxs/Workspaces/shopwell/sync-upstream`.
