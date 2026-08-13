---
name: apply-mve-frontend
description: Apply a reusable Minimum Viable Experience framework to frontend design, review, implementation, or refinement. Use when building pages, forms, dashboards, chat interfaces, admin workflows, mobile experiences, or multi-step journeys and the goal is to provide enough usability, support, confidence, inclusion, and satisfaction for users to complete their goal without understanding the underlying APIs, database, or data model.
---

# Apply MVE Frontend

Apply Minimum Viable Experience (MVE) as a user-outcome standard for frontend work. Treat a feature as successful only when a real user can understand it, complete the intended task, recover from problems, trust the result, and verify completion.

MVE is not merely the smallest working feature:

- MVP asks whether the capability exists.
- MVE asks whether the intended user can use it successfully and confidently.

## Operating principles

- Start from the user's goal and context, not the API, database, or component tree.
- Use business language in the primary journey; keep technical concepts secondary or hidden.
- Show one clear primary action at each step.
- Ask for the minimum information required to make progress.
- Use progressive disclosure for advanced options, maintenance controls, and governance detail.
- Make meaningful system states visible and truthful.
- Preserve user effort when requests fail or the connection is interrupted.
- Distinguish accepted, processing, completed, and verified outcomes.
- Finish with proof of the user's actual outcome and a useful next action.
- Keep existing advanced capabilities available unless the task explicitly removes them.
- Match the project's existing patterns and make the smallest scoped change that achieves the MVE outcome.

## Apply the workflow

### 1. Define the outcome

Write a short feature brief before designing or editing:

```text
Feature:
Primary user:
User context:
User goal:
Primary success outcome:
Primary action:
Minimum required information:
Technical concepts to hide or translate:
Completion proof:
Responsive and accessibility expectations:
Out of scope:
```

If the repository or request already provides this information, derive it from the source instead of inventing a new product direction.

### 2. Inspect the existing journey

For an existing application, inspect the relevant route, shared shell, components, data-loading code, capability or permission checks, and current tests before proposing changes. Trace the user journey from entry to completion, including:

```text
Entry -> orientation -> input/selection -> primary action -> progress -> review/confirmation -> completion -> next action
```

Record confusing terminology, unnecessary choices, hidden dependencies, missing states, data-loss risks, and places where the UI claims more than the backend has confirmed.

Do not infer that a backend capability exists from a frontend control. Treat the authoritative contract and confirmed runtime state as the source of truth.

### 3. Evaluate the eight MVE dimensions

Assess the feature against each dimension and identify the smallest high-value improvement.

1. **Goal clarity** - The user understands what the screen is for and what outcome is possible.
2. **Guided usability** - The next best action is obvious; the primary action is not competing with unnecessary choices.
3. **Simplicity** - The user does not need to understand API objects, IDs, versions, resource relationships, or internal workflow names.
4. **State visibility** - Loading, saving, draft, success, empty, unavailable, restricted, processing, and failure states are visible and understandable.
5. **Trust** - The interface explains relevant sources, permissions, certainty, status, confirmation, or receipts without overwhelming the primary journey.
6. **Recovery** - Validation, retry, reconnection, refresh, partial failure, and interruption paths preserve effort and provide actionable recovery.
7. **Inclusion** - The experience works for the intended roles, devices, viewport sizes, keyboard users, screen readers, touch users, and reduced-motion preferences.
8. **Completion** - The user can verify the real outcome and knows what to do next.

Use this compact score only as a diagnostic aid, not as a substitute for judgment:

```text
0 = missing or misleading
1 = present but weak or inconsistent
2 = clear, recoverable, and appropriate to context
```

### 4. Design the happy path and the state model

Model the experience as a sequence of user-facing states, not only a success path:

- Initial or empty state
- Input or selection state
- Validation state
- Loading or saving state
- Progress or queued state
- Review or confirmation state
- Success state
- Permission or capability-denied state
- Unavailable or dependency-failure state
- Recoverable failure state
- Partial-completion state
- Interrupted, reconnecting, or resumable state

For every remote mutation, decide what the user sees before, during, and after the request. Prevent duplicate submissions. Preserve entered values. If multiple operations are involved, track each result independently and never imply atomic success unless the system guarantees it.

### 5. Translate the interface

Prefer terms that describe the user's work:

- "Create a service" instead of "Create a service-page resource"
- "Choose a category" instead of "Select a section ID"
- "Review and publish" instead of "Execute publication mutations"
- "This action is waiting for confirmation" instead of "Status: accepted"

Keep implementation identifiers out of primary forms and messages. Explain technical details only when they help the user decide, recover, or meet a governance requirement.

### 6. Implement or recommend the smallest useful change

When implementation is authorized:

- Reuse the existing shell, components, contracts, state patterns, and terminology.
- Keep one primary action per step or surface.
- Add inline, field-level, and summary errors where appropriate.
- Add explicit loading and disabled states for remote work.
- Make recovery local to the failed step where possible.
- Add completion links, receipts, previews, or other proof appropriate to the outcome.
- Preserve advanced routes and workflows unless their removal is in scope.

When the user asks for review, requirements, or design only, do not modify production files. Report the MVE gaps and recommended changes instead.

### 7. Verify the experience

Verify in proportion to risk. At minimum, check:

- The primary happy path from entry to verifiable completion.
- Validation and empty states.
- A recoverable failure and retry path when feasible.
- Permission or unavailable behavior.
- Refresh or interruption behavior for multi-step work.
- Desktop and intended mobile or narrow viewport layouts.
- Keyboard focus, semantic labels, live status announcements, and touch target usability.
- That success messaging matches authoritative backend state.

Report unverified cases explicitly. Passing typecheck or rendering a page does not prove the user journey is complete.

## Reusable acceptance checklist

### Understanding

- Can a new user explain the purpose of the screen?
- Is the primary outcome stated in user language?
- Are technical concepts hidden, translated, or justified?

### Task completion

- Is the next action obvious?
- Is there one dominant action?
- Does the user provide only the minimum required information?
- Are advanced choices secondary?

### Feedback and trust

- Does the user know what the system is doing?
- Are status and progress understandable?
- Are sources, permissions, confirmations, or receipts shown where trust matters?
- Does the UI avoid claiming success before the result is verified?

### Resilience

- Are errors specific and actionable?
- Is entered information preserved?
- Can the user retry safely without duplicate mutations?
- Can the user recover after refresh, interruption, or partial completion?

### Completion and inclusion

- Is completion unmistakable?
- Can the user verify the actual outcome?
- Is the next useful action clear?
- Does the feature work across intended roles, devices, viewport sizes, and assistive technologies?

## Recommended response format

For an MVE review, report:

1. **Outcome:** What the user is trying to accomplish.
2. **Current journey:** The observed path and important states.
3. **MVE assessment:** Strengths and gaps across the eight dimensions.
4. **Priority improvements:** Smallest changes with the greatest user benefit.
5. **Verification:** What was tested and what remains unverified.

For implementation work, add the changed files and user-visible behavior to the verification section. Keep the report plain-language and outcome-led.

## MVE release gate

Do not call a feature MVE-ready when:

- The user must understand an API object or identifier to proceed.
- The next action is unclear.
- Loading or failure looks like a frozen or unexplained screen.
- A failed request unnecessarily erases user work.
- The UI claims success without evidence or authoritative confirmation.
- Permission restrictions appear as broken controls or misleading empty states.
- The feature works only at the developer's preferred viewport.
- The user cannot tell how to recover or what to do after completion.
