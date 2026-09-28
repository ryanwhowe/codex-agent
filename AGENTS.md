# Repository instructions

This repository distributes Codex instructions and skills. It has no application test suite.

## Validate skill changes

- After creating or changing a skill, run the skill-creator `quick_validate.py` against each changed skill directory. It validates `SKILL.md` but does not inspect `agents/openai.yaml`.
- Parse any changed `agents/openai.yaml` with PyYAML and verify its intended settings. For `work-with-me`, `policy.allow_implicit_invocation` must remain `false` so the skill requires explicit invocation.
- Use a disposable Docker container with PyYAML and keep validation dependencies out of this repository. Run from the repository root, mounting this repository and the skill-creator scripts read-only. This example validates both files for `work-with-me`; adapt the checks for other changed skills:

```sh
docker run --rm --entrypoint sh \
  --mount type=bind,src="$PWD",dst=/repo,readonly \
  --mount type=bind,src="$HOME/.codex/skills/.system/skill-creator/scripts",dst=/validator,readonly \
  --workdir /repo debian:trixie-slim \
  -c 'apt-get update -qq && DEBIAN_FRONTEND=noninteractive apt-get install -y -qq python3 python3-yaml >/dev/null && python3 /validator/quick_validate.py skills/work-with-me && python3 -c "import yaml; from pathlib import Path; config = yaml.safe_load(Path(\"skills/work-with-me/agents/openai.yaml\").read_text()); assert config[\"policy\"][\"allow_implicit_invocation\"] is False; print(\"Explicit-only policy valid\")"'
```

- If the skill-creator script is installed elsewhere, adjust the validator mount source. If Docker cannot pull the Debian image, use an available local Debian-based image and keep the same read-only mounts.
- Inspect the final diff and run `git diff --check`. The validator checks skill structure; it does not prove that the workflow behaves correctly.
