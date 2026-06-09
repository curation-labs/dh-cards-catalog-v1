# Curation Labs Darwinian Harness Cards Catalog V1

This repository is the public Git-backed card catalog for Darwinian Harness.

The `drwn` CLI reads the root `catalog.json` file to discover installable
Harness Cards. The catalog uses schema version 1:

```json
{
  "catalogVersion": 1,
  "scope": "@community",
  "description": "Curation Labs Darwinian Harness Cards Catalog V1",
  "cards": []
}
```

Each card entry must use an unscoped `name` and an installable Git card ref:

```json
{
  "name": "backend",
  "url": "git+https://github.com/example/backend-card.git#v1.0.0",
  "description": "Backend project harness",
  "tags": ["backend"],
  "stability": "stable",
  "lastValidatedWith": "0.2.1",
  "testStatusBadge": "https://img.shields.io/github/actions/workflow/status/example/backend-card/validate.yml"
}
```

Optional quality fields:

- `stability`: `experimental`, `stable`, or `production`.
- `lastValidatedWith`: strict semver for the `drwn` CLI version last used to validate the card.
- `testStatusBadge`: HTTPS badge URL for the card repo's validation workflow.

Users can register and search this catalog with:

```bash
drwn library catalog add https://github.com/curation-labs/dh-cards-catalog-v1.git
drwn search card backend --scope @community
```

Card producers can publish entries with:

```bash
drwn card catalog publish <card-ref> \
  --catalog https://github.com/curation-labs/dh-cards-catalog-v1.git \
  --mode direct
```

## Validation

This repo includes GitHub workflows for shallow PR validation and scheduled
deep validation through `curation-labs/drwn-validate-action@v1`. They run when
the repository variable `DRWN_VERSION` is set to a published
`darwinian-harness` version that includes `drwn catalog validate`.
