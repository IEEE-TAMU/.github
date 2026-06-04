# IEEE TAMU .github

Shared GitHub configuration for the [IEEE-TAMU](https://github.com/IEEE-TAMU) organization.

## Shared Workflows

### `docker-publish.yaml`

Reusable workflow for building and publishing Docker images from a `Dockerfile` to GHCR.

**Inputs:**

| Input | Required | Description |
|-------|----------|-------------|
| `image-name` | yes | Docker image name (e.g. `docs`, `portal`, `discord-bot`) |

**Usage:**

```yaml
jobs:
  publish:
    uses: IEEE-TAMU/.github/.github/workflows/docker-publish.yaml@master
    with:
      image-name: my-app
```

> `GITHUB_TOKEN` is automatically available in reusable workflows — no `secrets: inherit` needed unless you use custom secrets.

Used by: `docs`, `portal`, `discord`

---

### `nix-docker-publish.yaml`

Reusable workflow for building and publishing Docker images from a Nix flake to GHCR.

**Inputs:**

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `image-name` | yes | — | Docker image name (must match `name` set in the Nix flake's `dockerTools` call) |
| `flake-attr` | no | `packages.x86_64-linux.docker` | Nix flake attribute path to build |
| `stream` | no | `true` | `true` if the flake uses `streamLayeredImage`, `false` if it uses `layeredImage` |

**Usage:**

```yaml
jobs:
  publish:
    uses: IEEE-TAMU/.github/.github/workflows/nix-docker-publish.yaml@master
    with:
      image-name: my-app
```

> `GITHUB_TOKEN` is automatically available in reusable workflows — no `secrets: inherit` needed unless you use custom secrets.

Used by: `homepage`

**Flake example (streamLayeredImage, `stream: true`):**

```nix
packages.docker = pkgs.dockerTools.streamLayeredImage {
  name = "my-app";
  tag = "latest";
  contents = [ ... ];
  config = { ... };
};
```

**Flake example (layeredImage, `stream: false`):**

```nix
packages.docker = pkgs.dockerTools.layeredImage {
  name = "my-app";
  tag = "latest";
  contents = [ ... ];
  config = { ... };
};
```
