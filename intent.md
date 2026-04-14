# intent

This file is the stable reference for what this repository is for. Treat the headings below as link targets for commits, PRs, and the intent log.

## repo-purpose

This repository exists to keep personal host-level defaults small, reviewable, and portable across the machines I actually use.

It should make a new machine predictable to bootstrap with chezmoi, while keeping machine-specific identity data local at render time.

## non-goals

This repository is not meant to provision full development environments, install large toolchains, or hold secrets, private keys, or machine-specific state.

Dev Containers remain the preferred place for project-specific tooling.

## supported-environments

Expected to work for Windows with WSL2 and Ubuntu-like POSIX shells, with Git configured through chezmoi-managed dotfiles.

Assumptions:

- chezmoi is the apply mechanism
- login shells read `.profile`
- WSL host shells may use the Windows 1Password SSH agent
- Dev Containers should keep their own forwarded SSH agent socket

Windows-specific Git behavior belongs in the Windows fragment. POSIX and container-safe behavior belongs in the shared or POSIX fragments.

## risk-boundaries

Applying this repo may change files in the home directory that chezmoi manages, including Git config and shell profile behavior.

This repo should not:

- install packages automatically
- mutate system services or OS settings outside managed dotfiles
- write secrets or private keys into the repository
- override container SSH agent forwarding when a socket is already present

Any change that could break `chezmoi init`, `chezmoi status`, or `chezmoi apply` on a new machine is high risk and should be called out explicitly.

## good-outcomes

Good changes usually look like one of these:

- a fresh machine can render and apply without hand-editing tracked files
- shared Git defaults stay consistent while platform-specific behavior is isolated
- WSL host shells gain host integration without breaking Dev Containers
- prompts collect only local machine identity data that should not be committed

## update-intent

Update this file when the repository gains a new supported environment, changes bootstrap/apply assumptions, or moves a safety boundary.

Do not update it for routine value tweaks or small config adjustments unless they change what this repo is trying to optimize for.