# codex-agent

This repository contains shared instructions and a reusable skill for Codex. `CODEX_AGENTS.md` provides global preferences through a symlink at `~/.codex/AGENTS.md`. The `work-with-me` skill is loaded only when you explicitly invoke it.

## Setup

These instructions support Unix-like systems such as macOS and Linux.

### 1. Clone the repository

Clone this repository to the location you want to keep as the source of truth. The examples below use `<repository-path>` as a placeholder for that location.

### 2. Create the global-instructions symlink

Create the Codex directory if needed, then link the shared file as Codex's global `AGENTS.md`:

```sh
mkdir -p "$HOME/.codex"
ln -s "<repository-path>/CODEX_AGENTS.md" "$HOME/.codex/AGENTS.md"
```

If `~/.codex/AGENTS.md` already exists, skip the `ln` command. Do not use `ln -sf`. Keep the existing file or symlink; integrating these shared instructions with it is your responsibility.

Codex does not automatically load the repository's separately named `CODEX_AGENTS.md` file. It loads the linked file through the global `AGENTS.md` path unless a global `AGENTS.override.md` takes precedence.

### 3. Link the personal skill

To make the `work-with-me` workflow available in all projects on this machine, link its directory into the personal skills location:

```sh
mkdir -p "$HOME/.agents/skills"
ln -s "<repository-path>/skills/work-with-me" "$HOME/.agents/skills/work-with-me"
```

If `~/.agents/skills/work-with-me` already exists, skip the `ln` command and decide how to integrate it yourself. Do not use `ln -sf`. The skill is configured for explicit invocation only; saying `work with me` in ordinary text does not activate it. Invoke `$work-with-me` in Codex CLI or the IDE extension, or select the skill in the ChatGPT desktop app.

## Verify the setup

If you created the global-instructions symlink, confirm that it points to the repository copy:

```sh
test -L "$HOME/.codex/AGENTS.md"
readlink "$HOME/.codex/AGENTS.md"
```

The second command should print `<repository-path>/CODEX_AGENTS.md` (or the equivalent path you used).

If you created the skill symlink, confirm that it points to the repository's skill directory:

```sh
test -L "$HOME/.agents/skills/work-with-me"
readlink "$HOME/.agents/skills/work-with-me"
```

Start a new Codex session. Ask it to summarize its global instructions, then check the skill picker (or `/skills` in Codex CLI) for `work-with-me`. To check the workflow, explicitly invoke the skill with a task request and confirm that Codex presents a proposal for approval before editing.

## Update the shared instructions

Both symlinks point directly to the repository. To retrieve changes committed by others:

```sh
cd "<repository-path>"
git pull
```

Start a new Codex session to load the updated instructions and skill.

## Remove the symlinks

If you created these symlinks, remove each one only while it still points to this repository. This does not remove the repository files:

```sh
if [ -L "$HOME/.codex/AGENTS.md" ] &&
   [ "$(readlink "$HOME/.codex/AGENTS.md")" = "<repository-path>/CODEX_AGENTS.md" ]; then
  rm "$HOME/.codex/AGENTS.md"
fi
if [ -L "$HOME/.agents/skills/work-with-me" ] &&
   [ "$(readlink "$HOME/.agents/skills/work-with-me")" = "<repository-path>/skills/work-with-me" ]; then
  rm "$HOME/.agents/skills/work-with-me"
fi
```
