# Management of my dotFiles

This repository manages **host-level configuration** using [chezmoi].
Development environments are expected to be provided via **Dev Containers**.

---

## Recommended setup (Windows + WSL2)

1. Install WSL and Ubuntu
2. Install Docker Desktop and VS Code on Windows
3. Open an Ubuntu shell
4. Install chezmoi **inside Ubuntu**:

`sh -c "$(curl -fsLS get.chezmoi.io)"`

5. Initialize the repo:

`chezmoi init JohnyWS`

The first render will prompt once for your Git identity and SSH signing public key.
Those values stay local to the machine and are not committed back to this repository.

6. Review the rendered state:

`chezmoi status`

7. Apply changes:

`chezmoi apply -v`

Repositories should be cloned into `~/src` and opened from WSL using `code .`.

---

## SSH keys

Generate a unique SSH key per machine (recommended) and add the public key
to GitHub and 1Password as required.

Authentication and signing are intentionally separated:

- SSH authentication should come from the 1Password-backed SSH agent.
- Git signing should use a separate SSH public key configured as `user.signingkey`.
- No private keys or identity files are stored in this repository.
