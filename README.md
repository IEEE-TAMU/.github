# IEEE TAMU .github

Shared GitHub configuration for the [IEEE-TAMU](https://github.com/IEEE-TAMU) organization.

## Shared Workflows

- **`docker-publish.yaml`** — Reusable workflow for building and publishing Docker images to GHCR. Used by `docs`, `portal`, and `discord` repos.

### Usage

```yaml
jobs:
  publish:
    uses: IEEE-TAMU/.github/.github/workflows/docker-publish.yaml@main
    with:
      image-name: my-app
    secrets: inherit
```
