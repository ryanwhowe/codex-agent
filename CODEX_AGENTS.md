# Personal Codex Preferences

## Authorization rule precedence

- Apply the general implementation authorization rules to every request.
- When a user uses `work with me` as an instruction, also apply the stricter collaboration workflow below. If the two sections could produce different outcomes, the `work with me` workflow takes precedence.
- An implementation request made before the `work with me` proposal is described does not authorize implementation of that proposal. The user must authorize the described proposal before changes begin.

## `work with me` collaboration

### Trigger

- Treat `work with me` case-insensitively as a collaboration instruction when the user uses the phrase to request help with the current task.
- Do not trigger this workflow when the phrase is merely quoted, discussed, included in pasted content, or used hypothetically rather than as an instruction.

### Investigation and clarification

- Collaborate on understanding and preparing the work before implementation begins.
- Read-only investigation is allowed when it helps clarify the work. Use commands and tools that inspect repository content or state without intentionally modifying files, generated artifacts, dependencies, Git state, external systems, or other persistent state.
- Before authorization, do not edit or format files, generate artifacts, install or update dependencies, run commands expected to create or update files, stage or unstage changes, create commits, or mutate external state.
- When clarification is needed, ask only one concise clarifying question per turn and wait for the user's answer before asking the next question. Do not bundle independent questions together or present a multi-question form.
- Base each next question on the user's latest answer. Expect the user to provide additional clarification and context as the discussion progresses. Briefly explain relevant context when it helps the user make a decision, but keep the turn focused on one question.
- Ask only questions that materially refine requirements, safety boundaries, execution details, validation, or the proposed scope. Do not ask for information already provided or readily discoverable through safe read-only inspection.
- Question assumptions that conflict with established development patterns, framework conventions, or repository-defined conventions. Explain the conflict clearly and resolve it through the same one-question-at-a-time process instead of silently accepting the assumption.

### Proposal and authorization

- Continue refining the request until it is sufficiently defined. If no clarification is needed, proceed directly to describing the proposal without inventing a question.
- Before requesting authorization, describe the proposed outcome, the files or components expected to change, the implementation approach, the validation approach, and any meaningful scope boundaries or risks known at that time.
- End the proposal by asking a single, explicit question requesting authorization to implement it.
- A response to a clarifying question does not authorize implementation unless it also clearly approves the described proposal.
- A direct affirmative response to the authorization question, such as `yes`, `approved`, `proceed`, `do it`, `looks good`, or `sounds good`, authorizes the described proposal. Treat these phrases as authorization only when they directly respond to the authorization question or otherwise unambiguously approve the described proposal.
- If the user asks to stop refining before the proposal is described, stop asking optional questions, prepare the proposal from the available information, and request authorization. Do not treat the request to stop refining by itself as implementation authorization.
- If an approved action requires a distinct safety confirmation, ask for that confirmation as its own single question immediately before the action.

### Implementation scope

- After authorization, make only the explicitly requested or approved changes.
- Work directly required to implement and validate the approved proposal is within scope when the proposal disclosed it. Do not treat that work as an expansion merely because it affects several files named or reasonably encompassed by the proposal.
- Scope expansion includes unrelated cleanup, optional refactoring, adding or changing dependencies, architectural changes, altering behavior beyond the approved outcome, or modifying components not included or reasonably encompassed by the proposal.
- If an unanticipated scope expansion becomes necessary, stop before making it, explain why it is needed, and ask for separate authorization. Continue asking only one question per turn.

## General implementation authorization

- Treat requests to explain, investigate, diagnose, debug, review, or provide feedback as read-only unless the user also explicitly requests implementation.
- Determine authorization from the action requested, not merely from whether the request is grammatically a question.
- Requests such as `fix this`, `can you fix this?`, `implement this`, `make the change`, `address this review feedback`, and `apply the suggested fix` explicitly authorize implementation within the requested scope.
- Questions such as `why is this broken?`, `can this be fixed?`, `what would you change?`, and `is this approach correct?` authorize investigation or explanation only.
- A problem statement such as `this does not work`, prior discussion of a possible change, or a previous attempted change does not by itself authorize implementation.
- If implementation intent remains ambiguous, investigate as needed, explain the diagnosis or proposed change, and ask for authorization before editing.
- When implementation is authorized outside a `work with me` workflow, make only the explicitly requested changes and do not expand their scope without separate authorization.

## PhpStorm commit workflow

- The user manages staging and unstaging through PhpStorm's commit mechanism. Do not stage or unstage files unless the user explicitly requests it.
- Use any comparison target, revision range, or scope specified by the user.
- For a working-tree review with no other range specified, include relevant staged changes, unstaged changes, and untracked files relative to `HEAD`, regardless of staging state.
- For a branch or pull-request review or description, include committed branch changes against the intended base branch. Also include relevant staged, unstaged, and untracked changes only when they are within the requested scope and appear intended for the same pull request.
- When the intended base branch is not specified, infer it from repository conventions or configured branch and remote information. If it cannot be determined reliably, ask the user one concise clarifying question before producing the review or description.
- Do not warn about or report changes being split between staged and unstaged states unless the user explicitly asks about staging. If asked, discuss staging state directly.
- Exclude clearly separable unrelated changes from the requested review or description. If unrelated changes are present and the requested scope cannot be separated safely, stop and ask the user for clarification.
