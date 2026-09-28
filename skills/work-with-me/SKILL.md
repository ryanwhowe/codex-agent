---
name: work-with-me
description: Collaborate on a task through read-only investigation and one question at a time, then obtain approval of a concrete proposal before implementation. Use only when explicitly invoked.
---

# Work with me

## Scope

- Apply this workflow to the current task when this skill is explicitly invoked.
- This workflow takes precedence over general implementation authorization when the two could lead to different outcomes. An implementation request made before the proposal below is described does not authorize implementation of that proposal.

## Investigate and clarify

- Collaborate on understanding and preparing the work before implementation begins. Read-only inspection is allowed when it helps clarify the task.
- Before approval of the proposal, do not edit or format files, generate artifacts, install or update dependencies, run commands expected to create or update files, stage or unstage changes, create commits, or mutate external state.
- When clarification is needed, ask one concise question per turn and wait for the answer before asking another. Do not bundle independent questions or present a multi-question form. Base the next question on the latest answer.
- Ask only about matters that materially refine requirements, safety boundaries, execution details, validation, or scope. Use safe inspection to resolve facts that are readily discoverable. Explain and question assumptions that conflict with established development patterns or repository conventions.

## Propose and obtain approval

- When the request is sufficiently defined, describe the proposed outcome, expected files or components, implementation approach, validation approach, and meaningful scope boundaries or risks. Do not invent a question when no clarification is needed.
- End the proposal with one explicit question requesting authorization to implement it. Do not change persistent state before the user approves the described proposal.
- A reply to a clarifying question does not authorize implementation unless it also clearly approves the described proposal. A direct affirmative reply to the authorization question, such as `yes`, `approved`, `proceed`, `do it`, `looks good`, or `sounds good`, authorizes that proposal.
- If the user asks to stop refining before a proposal exists, stop optional questions, prepare the proposal from available information, and request authorization. The request to stop refining is not itself authorization.

## After approval

- Carry out the approved work under the general implementation-scope and validation rules.
- Ask one additional, action-specific confirmation immediately before an irreversible or externally consequential action, such as deleting data that cannot readily be restored, force-pushing, deploying to a live environment, or sending a message on the user's behalf. Ordinary workspace edits and routine local validation covered by the proposal need no second confirmation. Follow any approval required by the execution environment.
- When the approved proposal includes an explicit request to create a feature branch, push changes, and create a pull request, the necessary staging, commit, ordinary push, and pull-request creation need no additional confirmation. Force-pushing and merging remain separate actions.
