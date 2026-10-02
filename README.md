# `shopwell-shop/octo-sts-action`

This is a fork of [octo-sts/action](https://github.com/octo-sts/action), that supports self-hosted instances with a fallback to the official octo-sts.

This action federates the GitHub Actions identity token for a Github App token
according to the Trust Policy in the target organization or repository.

## Usage

```yaml
permissions:
  id-token: write # Needed to federate tokens.

steps:
- uses: shopwell-shop/octo-sts-action@main
  id: octo-sts
  with:
    scope: your-org/your-repo
    identity: foo
    self_hosted_domain: ${{ secrets.OCTO_STS_DOMAIN }}

- env:
    GITHUB_TOKEN: ${{ steps.octo-sts.outputs.token }}
  run: |
    gh repo list
```

The above will load a "trust policy" from `.github/chainguard/foo.sts.yaml` in
the repository `your-org/your-repo`.  Suppose this contains the following, then
workflows in `my-org/my-repo` will receive a token with the specified
permissions on `my-org/my-repo`.

The `self_hosted_domain` input is the domain to the self-hosted instance. We have a organization-wide secret, which always contains the current domain.

```yaml
issuer: https://token.actions.githubusercontent.com
subject: repo:my-org/my-repo:ref:refs/heads/main

permissions:
  contents: read
  issues: write
```

See the [Use Action](./.github/workflows/use-action.yaml) workflow for a working example of this, that opens an issue in this repository.
