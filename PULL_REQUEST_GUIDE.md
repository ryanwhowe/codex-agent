# Pull Request Guide

Use this guide when drafting, updating, or creating a GitHub pull request for Ryan Howe. Follow repository-local instructions and pull request templates first; use this guide for decisions they do not settle.

## Before writing

- Confirm the authenticated GitHub user is Ryan Howe's account and include only pull requests or changes within the requested scope.
- Determine the intended base from the user's request, pull request metadata, the remote default branch, or an unambiguous repository convention, in that order. Do not assume the feature branch's upstream is the pull request base.
- Resolve the base according to the shared instructions, compute the merge base, and inspect the complete change from that merge base through `HEAD`.
- Include relevant staged, unstaged, and untracked work when it is intended for the same pull request. Do not stage or unstage it.
- Read the commit subjects and bodies, branch name, linked ticket context that is already available, repository instructions, and the repository's current pull request template.
- Separate substantive behavior from mechanical changes such as renames, formatting, generated output, or namespace updates.
- Identify release operations, migrations, compatibility concerns, production evidence, testing, and documentation that are actually supported by the available context.
- If a required fact cannot be learned from the changes or available context, ask rather than inventing it. This especially applies to production data, release timing, manual SQL, test results, and operational impact.

## Classify the pull request

Choose the first matching pattern before drafting the title or body.

### Environment promotion

An environment promotion merges already-reviewed work into a branch such as `demo` or another deployment environment.

- Use the terse title `<target environment> <release ticket>`.
- Leave the body empty unless the repository or user explicitly requires release content.
- Do not repeat the descriptions of the bundled feature pull requests.

Example: `demo 32610`

### Revert

- Preserve GitHub's conventional revert title and body when they accurately identify the reverted pull request.
- Do not replace a concise generated explanation with the normal feature template.

### Retry or replacement

A retry recreates a previously merged or reverted change after an operational failure.

- Open with a short reference to the earlier pull request and explain why another pull request is needed.
- Put required recovery or release instructions in an active caution block.
- Emphasize information that prevents the failure from recurring, even when the code diff matches the earlier pull request.

### Normal development change

Use the repository template and the style rules below for features, fixes, refactors, form updates, migrations, and testing changes.

## Title

- For ticketed ePay work, use `<ticket ID> - <short change summary>`.
- Prefer the established commit subject when it accurately represents the whole pull request.
- Keep the summary direct and specific. Match established project capitalization and terminology rather than imposing a new title convention.
- Use the change's primary purpose, not a list of files or implementation steps.
- For reverts and environment promotions, use their specialized title rules instead.

## Description

- Preserve the repository template's headings, comments, link format, type section, and checklist unless a specialized pull request pattern calls for an empty or generated body.
- Replace the template's instructional description text; do not leave it as visible prose.
- Start with the purpose or outcome of the change.
- For a narrow change, prefer one compact sentence or paragraph. Do not enumerate details merely because they are visible in the diff.
- For a change with several reviewer-relevant behaviors, use one lead sentence followed by a short bullet list. Each bullet should describe a distinct outcome, compatibility guarantee, test addition, or meaningful refactor.
- Explain motivation or production context when it helps reviewers understand why the change exists.
- Mention implementation details only when they affect review, deployment, compatibility, or future maintenance.
- Wrap code identifiers, command names, filenames, and literal error text in backticks.
- Preserve project vocabulary and capitalization, including names such as ePay, ePOS, eMobile, ClickUp, Symfony, and YAML.
- Do not inflate a narrow form or wording change into a technical inventory. A description such as `Updated/corrected wording on Death Certificate` can be sufficient when it fully states the reviewer-relevant outcome.
- Do not claim tests passed, documentation changed, behavior is backward-compatible, or a release is safe unless the available evidence supports the claim.

## Operational and release context

Use an active GitHub caution block when reviewers or release operators must act on the information.

```md
> [!CAUTION]
> Required release or operational instruction.
```

Appropriate caution content includes:

- SQL that must run before or after release;
- cache clearing or another recovery step required to avoid a known failure;
- an explicit release order, release date, or deployment dependency;
- confirmation that a test-runner-only change does not require an application release;
- another concrete instruction that changes how the pull request should be merged or deployed.

Do not infer operational requirements from suggestive code or dates. Activate the warning only when the requirement is established by the ticket, user, repository documentation, prior failure, or other available evidence.

### Database changes

- Check for a committed migration or another repository-standard schema mechanism.
- When ePay changes persisted schema without a committed migration, include the required executable SQL in an active caution block and state when it must run.
- Account for existing production data when the available context provides the necessary values.
- Never fabricate production rows or migration data. Ask for missing values before presenting the pull request as ready.
- Select `New Database Migration` and also `Refactor` when the change replaces an existing storage mechanism.

### Testing-only changes

- Distinguish ordinary automated tests from diagnostic commands or application test runners.
- Use the repository's established `Additional Testing` type when applicable, even if the current template requires adding that historical/custom option.
- If the change affects only internal validation and needs no application release, say so in an active caution block when that is known.

## Ticket link

- Preserve the repository template's link label and URL structure.
- For ePay, replace `TICKET_ID` with the ClickUp ticket identifier.
- Prefer the ticket encoded by the feature or release branch for the link. This may intentionally differ from a commit-derived title when a release branch contains work from another ticket.
- Do not silently reconcile conflicting ticket identifiers. If the correct link cannot be determined from an established branch convention, ask.

## Type of change

- Keep only applicable options and preserve their exact repository wording.
- Select the smallest accurate set; do not list every category that could loosely describe the diff.
- Use `Town Form Update` alone for a narrow municipality form or wording update unless another category is explicitly required.
- Use `Refactor` for structural changes without intended behavior changes.
- Use `Infrastructure Change` when deployment, framework wiring, or runtime infrastructure is materially affected.
- Use `New Database Migration` for schema changes, with `Refactor` as an additional type when an existing persistence mechanism is replaced.
- Use `Additional Testing` for changes whose deliverable is added diagnostic or validation coverage.
- Never invent a release-date classification solely because user-facing content contains a date.

## Checklist

- Preserve the template's checklist text and ordering.
- Mark an item complete only when the changes or known validation support it.
- Do not claim documentation changes solely to reproduce a historical pattern. If a required checklist statement is untrue, leave it unchecked and call it out before creating the pull request.

## Final review before creation

Before running a command that creates or updates a pull request:

1. Re-read the title and description against the diff, commits, branch ticket, and template.
2. Confirm the selected pull request pattern and base branch.
3. Remove file-by-file narration and details that do not help review or release.
4. Confirm every factual claim, checklist mark, test statement, and operational instruction has evidence.
5. Verify that all substantive reviewer-relevant outcomes are covered.
6. Check that the result follows the repository-specific voice: terse for narrow work, scoped bullets for genuinely multi-part work, and prominent cautions for known operational requirements.
7. Show the proposed title and body to the user before creating or updating the pull request when authorization has not already covered the exact external action.
