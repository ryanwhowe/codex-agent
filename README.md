# codex-agent

This repository contains shared instructions for Codex. The `CODEX_AGENTS.md` file is intended to be reused across multiple development environments and projects through a symlink in a user's `~/.codex` directory.

## Setup

These instructions support Unix-like systems such as macOS and Linux.

### 1. Clone the repository

Clone this repository to the location you want to keep as the source of truth. The examples below use `<repository-path>` as a placeholder for that location.

### 2. Create the shared-instructions symlink

Create the Codex directory if needed, then link the shared file into it:

```sh
mkdir -p "$HOME/.codex"
ln -s "<repository-path>/CODEX_AGENTS.md" "$HOME/.codex/CODEX_AGENTS.md"
```

The command intentionally uses a distinct name so an existing `~/.codex/AGENTS.md` is preserved. Do not use `ln -sf` for this setup; it could replace an existing file or symlink.

### 3. Reference the shared file from the existing AGENTS file

If `~/.codex/AGENTS.md` already exists, keep its contents and add an instruction telling Codex to read and follow the shared file:

```md
- Read and follow `~/.codex/CODEX_AGENTS.md`.
```

If there is no existing `~/.codex/AGENTS.md`, the `CODEX_AGENTS.md` symlink remains available as a separately named shared instruction file. Preserve any other instructions already configured in the Codex directory.

## Verify the setup

Confirm that the new path is a symlink and points to the repository copy:

```sh
test -L "$HOME/.codex/CODEX_AGENTS.md"
readlink "$HOME/.codex/CODEX_AGENTS.md"
```

The second command should print `<repository-path>/CODEX_AGENTS.md` (or the equivalent path you used).

## Update the shared instructions

The symlink points directly to the repository file, so updates are available to Codex automatically after the repository copy changes. To retrieve changes committed by others:

```sh
cd <repository-path>
git pull
```

## Remove the symlink

To stop using the shared instructions, remove only the symlink. This does not remove the repository file or the existing `~/.codex/AGENTS.md`:

```sh
rm "$HOME/.codex/CODEX_AGENTS.md"
```
