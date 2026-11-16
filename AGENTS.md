# AGENTS.md

Instructions for AI agents working in this repository. Read `intent.md` before changing anything; its headings are the anchors that commits, PRs and `intent-log.md` cite.

## This repository is public

Everything you push is public and permanent: files, commit messages, branch names, PR titles and descriptions, review comments and validation evidence. See `intent.md#public-repository`.

Before every commit, push and PR edit, check that none of these appear:

- secrets, private keys, tokens, 1Password item references
- email addresses, usernames, hostnames, machine IDs
- real local paths: home directories, repository roots, the private-identity prefix. Use placeholders (`<home>`, `<private-root>`)
- employer-internal names, URLs, projects or tooling

Machine-specific values belong in chezmoi prompts (`promptStringOnce` in `.chezmoi.yaml.tmpl`), never in tracked files. Write validation evidence as outcomes ("a repo under the private root resolves the private email"), not values.

A quick check before pushing:

```sh
git diff origin/main... | grep -nEi '@[a-z0-9-]+\.[a-z]|/users/|/home/[a-z]|c:[/\\]|ssh-(ed25519|rsa) |op://'
```

If something has already been pushed, stop and tell the user. Don't try to fix it silently with a force-push.

## Payload vs meta

Only payload (git, jj and shell config and their fragments) renders into `$HOME`. Meta files (this file, `intent.md`, `intent-log.md`, `README.md`, `ai-prompting/`) must be listed in `.chezmoiignore`. A new meta file without an ignore entry is a defect. See `intent.md#payload-vs-meta`.

## Changes

- Both native Windows and WSL must keep working (`intent.md#supported-environments`). Windows-only behaviour goes in the Windows fragment, POSIX behaviour in the POSIX fragment.
- Changes to identity switching or commit signing are high risk. Include validation evidence for both environments in the PR, and keep the PR a draft until both have been checked.
- Never edit rendered files in `$HOME`. Edit the source here and run `chezmoi apply`. To test one file without touching the others, use `chezmoi apply <target>`.
- Log material changes in `intent-log.md` (format and threshold are at the top of that file). Only append; never reorder earlier entries.

## Stacked PRs

Use stacked PRs when one change depends on another, or when two open changes would edit the same lines. `intent-log.md` is the usual case: every PR that logs appends to its end, so parallel PRs conflict.

- Base each PR's branch on the branch below it, not on `main`. Set the PR's base to that branch.
- Link the stack on GitHub bottom to top: `gh stack link <bottom-branch> <next-branch> <top-branch>`.
- When a lower PR changes, rebase the branches above it, then push with `--force-with-lease`. Force-pushing is fine on your own open PR branches, never on `main`.
- Merge from the bottom up.
