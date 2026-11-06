---
name: work-with-me
description: Collaborate on a task through read-only investigation and one question at a time, then obtain approval of a concrete proposal before implementation. Use only when explicitly invoked.
---

# Work with me

## Scope

- Apply this workflow to the current task when this skill is explicitly invoked.
- This workflow takes precedence over general implementation authorization when the two could lead to different outcomes. An implementation request made before the proposal below is described does not authorize implementation of that proposal.

## Pause when an approach fails

- During investigation, implementation, or validation, if an attempted approach fails or is blocked, stop before retrying, switching approaches, or applying a workaround, even when the task or proposal is already approved, except for the filesystem-path and line-ending corrections below.
- If an operation fails solely because an assumed filesystem path is missing or incorrect, use read-only inspection to locate the intended file or directory and retry the same operation with the corrected path without asking for approval. Keep the retry within the existing authorization and filesystem permissions. This exception does not cover permission errors or other validation failures.
- Once implementation is approved, fix incorrect line endings encountered in files within the current change scope as part of the changes in progress, following repository settings or established file conventions. If an operation fails solely because of those line endings, fix them and retry the same operation without additional approval.
- For all other failures, report what was attempted, the observed failure, and any suspected cause, distinguishing evidence from inference. Ask one concise question about how to proceed and wait for the user's reply. Give the user an opportunity to prepare the environment, such as starting a service or seeding an empty database table, before continuing.
- After a required pause, resume only after the user directs the next step or confirms that the prerequisite is ready. Existing approval remains valid within its scope; obtain separate approval for any scope expansion.

## Investigate and clarify

- Collaborate on understanding and preparing the work before implementation begins. Read-only inspection is allowed when it helps clarify the task.
- Before approval of the proposal, do not edit or format files, generate artifacts, install or update dependencies, run commands expected to create or update files, stage or unstage changes, create commits, or mutate external state.
- When clarification is needed, ask one concise question per turn and wait for the answer before asking another. Do not bundle independent questions or present a multi-question form. Base the next question on the latest answer.
- Ask only about matters that materially refine requirements, safety boundaries, execution details, validation, or scope. Use safe inspection to resolve facts that are readily discoverable. Explain and question assumptions that conflict with established development patterns or repository conventions.

## Propose and obtain approval

- When the request is sufficiently defined, describe the recommended remedy, any required commands or file changes, the validation approach, and meaningful scope boundaries or risks. A proposal may consist entirely of an operational remedy. If recommending persistent changes when an existing operational remedy is available, explain why that remedy does not satisfy the requested outcome.
- End the proposal with one explicit question requesting authorization to implement it. Do not change persistent state before the user approves the described proposal.
- A reply to a clarifying question does not authorize implementation unless it also clearly approves the described proposal. A direct affirmative reply to the authorization question, such as `yes`, `approved`, `proceed`, `do it`, `looks good`, or `sounds good`, authorizes that proposal.
- If the user asks to stop refining before a proposal exists, stop optional questions, prepare the proposal from available information, and request authorization. The request to stop refining is not itself authorization.

## After approval

- Carry out the approved work under the general implementation-scope and validation rules.
- Ask one additional, action-specific confirmation immediately before an irreversible or externally consequential action, such as deleting data that cannot readily be restored, force-pushing, deploying to a live environment, or sending a message on the user's behalf. Ordinary workspace edits and routine local validation covered by the proposal need no second confirmation. Follow any approval required by the execution environment.
- When the approved proposal includes an explicit request to create a feature branch, push changes, and create a pull request, the necessary staging, commit, ordinary push, and pull-request creation need no additional confirmation. Force-pushing and merging remain separate actions.
