# silverbluenix &nbsp; [![bluebuild build badge](https://github.com/esteve/silverbluenix/actions/workflows/build.yml/badge.svg)](https://github.com/esteve/silverbluenix/actions/workflows/build.yml)

Fedora Silverblue Atomic Desktop with Nix package manager and curated extras, signed and bootc-compatible.

## Variants

| Image | Base | Includes |
|-------|------|----------|
| `silverbluenix` | `silverblue-main` (latest) | Nix |
| `silverbluenix-gts` | `silverblue-main` (GTS/stable) | Nix |
| `silverbluenix-extras` | `silverbluenix` | Nix + common modules (Brave, Tailscale, Fish, keyd, etc.) |
| `silverbluenix-gts-extras` | `silverbluenix-gts` | Nix + common modules |

## Installation

First switch to the unsigned image to install the signing key and policy:

```
bootc switch ghcr.io/esteve/silverbluenix
```

Reboot:

```
systemctl reboot
```

Then switch again with signature enforcement enabled:

```
bootc switch --enforce-container-sigpolicy ghcr.io/esteve/silverbluenix
```

Reboot once more:

```
systemctl reboot
```

For future updates:

```
bootc upgrade
```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## ISO

If build on Fedora Atomic, you can generate an offline ISO with the instructions available [here](https://blue-build.org/how-to/generate-iso/#_top). These ISOs cannot unfortunately be distributed on GitHub for free due to large sizes, so for public projects something else has to be used for hosting.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/esteve/silverbluenix
```
