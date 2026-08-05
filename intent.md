# intent

This file is the stable reference for what this repository is for. Treat the headings below as link targets for commits, PRs, and the intent log.

## repo-purpose

This repository exists to keep personal host-level defaults small, reviewable, and portable across the machines I actually use.

It should make a new machine predictable to bootstrap with chezmoi, while keeping machine-specific identity data local at render time.

## non-goals

This repository is not meant to provision full development environments, install large toolchains, or hold secrets, private keys, or machine-specific state.

Dev Containers remain the preferred place for project-specific tooling.

## supported-environments

Expected to work as a first-class experience on **both** native Windows and WSL2 / Ubuntu-like POSIX shells, with Git configured through chezmoi-managed dotfiles. Neither environment is a fallback for the other; a change is not done until it holds in both.

Assumptions:

- chezmoi is the apply mechanism
- POSIX login shells read `.profile`
- WSL host shells may use the Windows 1Password SSH agent
- native Windows shells use the Windows-native 1Password mechanism directly
- Dev Containers should keep their own forwarded SSH agent socket

Not validated by default:

- native macOS hosts
- non-bash POSIX login shell behavior

Windows-specific Git behavior belongs in the Windows fragment. POSIX and container-safe behavior belongs in the shared or POSIX fragments. Behavior common to both belongs in the shared fragment.

## identity-switching

A single machine may host repositories that require different Git identities — for example a default work identity and a separate private identity. The repo supports selecting identity by repository context (such as a directory prefix), so the correct identity applies automatically without per-repo hand-configuration.

The value that selects context (which prefix maps to which identity) is machine-specific and must be collected at render time, never committed. A machine with no such split leaves it unset, and the default identity applies everywhere.

This is a host-level concern on the native-Windows side, where repositories share a common root and are not naturally isolated. POSIX/WSL setups that isolate identity per repository need not use it.

## commit-signing

Commit signing must work in **both** supported environments. Both sign with the same public signing key, backed by 1Password, but reach it through each environment's native mechanism — the anchor does not fix which mechanism, only that signing succeeds in both without divergent keys. Signing is a portability- and risk-sensitive concern: a change that breaks signing on either side is high risk (see risk-boundaries).

## risk-boundaries

Applying this repo may change files in the home directory that chezmoi manages, including Git config and shell profile behavior.

This repo should not:

- install packages automatically
- mutate system services or OS settings outside managed dotfiles
- write secrets or private keys into the repository
- override container SSH agent forwarding when a socket is already present

Any change that could break `chezmoi init`, `chezmoi status`, or `chezmoi apply` on a new machine is high risk and should be called out explicitly.

For high-risk changes, include brief validation evidence in the PR (for example, status/render/apply checks on a representative machine).

## good-outcomes

Good changes usually look like one of these:

- a fresh machine can render and apply without hand-editing tracked files
- shared Git defaults stay consistent while platform-specific behavior is isolated
- WSL host shells gain host integration without breaking Dev Containers
- prompts collect only local machine identity data that should not be committed
- the correct Git identity applies automatically per repository context, with the selecting value kept local
- commit signing keeps working in both native Windows and WSL after a change, verified on the affected side

## update-intent

Update this file when the repository gains a new supported environment, changes bootstrap/apply assumptions, or moves a safety boundary.

Heading stability rule: keep existing top-level headings stable. Prefer adding new headings over renaming existing ones, and note any unavoidable rename in `intent-log.md`.

Do not update it for routine value tweaks or small config adjustments unless they change what this repo is trying to optimize for.