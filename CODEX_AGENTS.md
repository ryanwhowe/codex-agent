## `work with me` collaboration

- When the user includes the phrase `work with me` in a request, use a deliberate single-question collaboration before making material changes.
- Ask exactly one concise question per turn. Do not bundle independent questions together or present a multi-question form.
- Base each next question on the user's latest answer. Briefly explain relevant context when it helps the user make the decision, but keep the turn focused on one question.
- Ask only questions that materially refine requirements, safety boundaries, execution details, or validation. Do not ask for information already provided or readily discoverable from safe repository inspection.
- Continue one question at a time until the request is sufficiently defined. Then state the resulting approach and carry it out without asking an unnecessary “ready to proceed” question.
- If an action still requires a distinct safety confirmation, ask that confirmation as its own single question immediately before the action.
- If the user asks to stop refining or tells you to proceed, stop asking optional questions and act on the information available.

## Explicit implementation authorization

- Treat questions, diagnosis, debugging reports, and feedback about an existing change as read-only by default. Do not modify source code, configuration, tests, or agent instructions unless the user explicitly asks to implement, fix, change, or update something.
- Do not infer implementation authorization from context, from a prior attempted change, or from wording such as “can we” or “this does not work.” Requests such as “address this review feedback” and “apply the suggested fix” are explicit implementation authorization. When the desired implementation is not explicit, explain the diagnosis and ask for authorization before editing.
- If the user explicitly authorizes a change, make only the smallest requested change and do not expand its scope without separate authorization.

## PhpStorm commit workflow

- The user manages staging and unstaging through PhpStorm's commit mechanism. For a requested review or PR description, consider staged and unstaged changes within the requested scope regardless of staging state. Do not warn about or report changes being split between staged and unstaged states unless the user explicitly asks about staging. If unrelated changes are present and the requested scope cannot be separated safely, stop and ask for clarification.
