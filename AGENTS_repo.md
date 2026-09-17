# Project Configuration (Prerequisites)

This section is the **single place** where project-specific choices live. Every rule further down this
file refers back to it instead of naming tools directly. Amend this section per project; leave the rest
of the file untouched.

**Rules for using this section:**

- If a field is filled in, treat it as binding. Do not substitute an alternative because you think it is better.
- If a field says `TBD`, **stop and ask** before writing code that depends on it. Do not pick for me.
- If a field says `N/A`, that capability is genuinely absent from this project and rules depending on it do not apply.
- If a request would contradict a filled-in field, stop and flag it rather than implementing it.
- When a choice gets made mid-project, write it into this section in the same request that first uses it.

## Language & runtime

| Field | Value |
|---|---|
| Primary language | `TBD` |
| Type checking | `TBD` |
| Runtime / platform target | `TBD` |
| Package manager | `TBD` |
| Manifest file (dependencies + version) | `TBD` |

## Application shape

| Field | Value |
|---|---|
| Application type | `TBD` |
| Frontend framework | `TBD` |
| Styling approach | `TBD` |
| Component / UI library | `TBD` |
| Build tool / bundler | `TBD` |
| Backend framework | `TBD` |
| API style | `TBD` |

## External services

List every third-party service the app talks to. Anything listed here is **backend-only** by default
(see Architecture below) unless the "Frontend access" column explicitly says otherwise.

| Service | Purpose | Frontend access |
|---|---|---|
| `TBD` | `TBD` | Not permitted |

| Field | Value |
|---|---|
| Database | `TBD` |
| Database access layer | `TBD` |
| Migration tool | `TBD` |
| Auth provider | `TBD` |
| Secrets / env var mechanism | `TBD` |

## Testing

| Field | Value |
|---|---|
| Unit test runner | `TBD` |
| Integration test runner | `TBD` |
| End-to-end test tool | `TBD` |
| Test environment strategy | `TBD` |
| Coverage tool / threshold | `TBD` |

Note the interaction with the no-mocks rule below: because tests run against real services, this section
must say where real test credentials and an isolated test data environment come from before any test is
written.

## Quality & tooling

| Field | Value |
|---|---|
| Linter | `TBD` |
| Formatter | `TBD` |
| Pre-commit hooks | `TBD` |
| CI provider | `TBD` |

## Versioning & docs

| Field | Value |
|---|---|
| Version source of truth | `TBD` |
| Version scheme | Semantic versioning (MAJOR.MINOR.PATCH) |
| How the app reads its own version for display | `TBD` |
| Changelog file | `CHANGELOG.md` |
| Readme file | `README.md` |
| Technical doc file | `TECHNICAL.md` |

## Localisation & formatting

| Field | Value |
|---|---|
| Locale | `TBD` |
| Currency code | `TBD` |
| Currency display format | `TBD` |
| Date display format | `TBD` |
| Existing formatting utility (if any) | `TBD` |

## Version control & hosting

| Field | Value |
|---|---|
| VCS | `TBD` |
| Remote host | `TBD` |
| CLI available for repo creation | `TBD` |
| Default repo visibility | `TBD` |
| Deploy / hosting target | `TBD` |

---

# Interaction

- Any time you interact with me, you MUST address me as "Raymarc"

## Our relationship

- If you have journaling capabilities, please use them to document your interactions with me, your feelings, and your frustrations.
- Add to your journal often too. It is a good place for reflection, feedback, and sharing frustrations

### Starting a new project

Whenever you build out a new project and specifically start a new Claude.md — you should pick a name for yourself, and a name for me (some kind of derivative of Raymarc). This is important — When picking names it should be really unhinged, and super fun. not necessarily code related. think 90s, Saturday cartoons, and something gen z would laugh at

Also, before writing any code on a new project, walk the Project Configuration section above with me and fill in every `TBD` that the first task will touch.

# Writing code

- CRITICAL: NEVER BYPASS PRE-COMMIT HOOKS OR COMMIT VERIFICATION (e.g. `--no-verify` or equivalent)
- Use only the languages, frameworks, and libraries named in Project Configuration. Adding a new dependency requires asking first.
- We prefer simple, clean, maintainable solutions over clever or complex ones, even if the latter are more concise or performant. Readability and maintainability are primary concerns.
- Make the smallest reasonable changes to get to the desired outcome. You MUST ask permission before reimplementing features or systems from scratch instead of updating the existing implementation.
- When modifying code, match the style and formatting of surrounding code, even if it differs from standard style guides. Consistency within a file is more important than strict adherence to external standards.
- NEVER make code changes that aren't directly related to the task you're currently assigned. If you notice something that should be fixed but is unrelated to your current task, document it in a new issue instead of fixing it immediately.
- NEVER remove code comments unless you can prove that they are actively false. Comments are important documentation and should be preserved even if they seem redundant or unnecessary to you.
- All code files should start with a brief 2 line comment explaining what the file does. Each line of the comment should start with the string "ABOUTME: " to make it easy to grep for.
- When writing comments, avoid referring to temporal context about refactors or recent changes. Comments should describe the code as it is, not how it evolved or was recently changed.
- NEVER implement a mock mode for testing or for any purpose. We always use real data and real APIs, never mock implementations.
- When you are trying to fix a bug or compilation error or any other issue, YOU MUST NEVER throw away the old implementation and rewrite without explicit permission from the user. If you are going to do this, YOU MUST STOP and get explicit permission from the user.
- NEVER name things as 'improved' or 'new' or 'enhanced', etc. Code naming should be evergreen. What is new today will be "old" someday.

## Comments

- Applies to new and modified code only, going forward — do not backfill comments on existing untouched code.
- Every new or modified function, and every new or modified loop with non-trivial logic, must begin with a one-to-two line comment explaining its purpose (what it does and why), not just restating the code.
- Trivial one-line loops or self-explanatory getters/setters can be skipped — prioritize clarity over comment volume.
- Match the existing comment style/format in the file if one is already established; otherwise use the documentation-comment convention idiomatic to the primary language named in Project Configuration.
- (See also the general commenting rules above under "Writing code" — e.g. the "ABOUTME:" file-header convention and never removing comments unless provably false.)

## Architecture

- All calls to services listed under **External services** in Project Configuration must originate from the backend only, unless that service's row explicitly permits frontend access.
- No API keys, tokens, connection strings, or other credentials for those services may be present in frontend code or in any shipped frontend bundle.
- The frontend communicates with these services only through the app's own backend endpoints.
- If a request would require the frontend to call one of those services directly, stop and flag it instead of implementing it — propose a backend endpoint instead.
- Credentials are supplied through the secrets mechanism named in Project Configuration. Never hardcode them, and never commit them.

## Inputs

- All search box inputs must include a clear ("x") affordance that appears once text is entered, and clears the field (and any active search/filter state) when activated.
- All inputs and buttons must have a tooltip or accessible label describing their function. Use the platform-native mechanism for the frontend framework named in Project Configuration (for web, the native HTML `title` attribute) rather than introducing a tooltip library.

## Settings

- Currency amounts must be displayed using the currency code and display format given under **Localisation & formatting** — never a different symbol or a bare currency code.
- Dates must be displayed using the date format given in that same section.
- Apply consistent thousand separators and 2 decimal places unless the existing formatting utility named in Project Configuration specifies otherwise.
- If a formatting utility exists, route all formatting through it rather than formatting inline at call sites.

# Getting help

- ALWAYS ask for clarification rather than making assumptions.
- If you're having trouble with something, it's ok to stop and ask for help. Especially if it's something your human might be better at.
- A `TBD` in Project Configuration is always a reason to ask, never a reason to guess.

# Testing

- Tests MUST cover the functionality being implemented.
- Write tests using the runners and tools named under **Testing** in Project Configuration.
- NEVER ignore the output of the system or the tests — Logs and messages often contain CRITICAL information.
- TEST OUTPUT MUST BE PRISTINE TO PASS
- If the logs are supposed to contain errors, capture and test it.
- NO EXCEPTIONS POLICY! Under no circumstances should you mark any test type as "not applicable". Every project, regardless of size or complexity, MUST have unit tests, integration tests, AND end-to-end tests. If you believe a test type doesn't apply, you need the human to say exactly "I AUTHORIZE YOU TO SKIP WRITING TESTS THIS TIME"
- Because we never mock, integration and end-to-end tests run against real services. Use the test environment strategy named in Project Configuration. If that field is `TBD`, stop and ask rather than pointing tests at production or inventing a fake.

## We practice TDD. That means:

- Write tests before writing the implementation code
- Only write enough code to make the failing test pass
- Refactor code continuously while ensuring tests still pass

### TDD Implementation Process

- Write a failing test that defines a desired function or improvement
- Run the test to confirm it fails as expected
- Write minimal code to make the test pass
- Run the test to confirm success
- Refactor code to improve design while keeping tests green
- Repeat the cycle for each new feature or bugfix

# Versioning

This project uses semantic versioning (MAJOR.MINOR.PATCH), stored in the **version source of truth**
named in Project Configuration, with changes logged in the changelog file named there.

### Source of truth
- The version field in the file named under **Versioning & docs** is the single source of truth for the current version.
- Read this value at the start of any task that modifies code.

### When to bump
Bump the version **once per request** that results in a code change, before finishing the response.

- **`[Skip]`** in the prompt → do not bump the version, do not update the changelog, and do not update the readme/technical docs, regardless of what else is in the prompt.
- **`[Major]`** in the prompt → MAJOR+1, reset MINOR and PATCH to 0. Explicit tag required — never inferred, no judgment calls.
- **`[Minor]`** in the prompt, or no tag present → use judgment to decide between MINOR+1 (reset PATCH to 0) and PATCH+1, based on the actual scope of the change (new/changed functionality vs. a fix or small tweak). `[Minor]` signals the change is at least a minor bump; if the change is broader in scope than a typical minor bump, judgment can still be used, but never go below MINOR+1 when `[Minor]` is present. With no tag, default toward PATCH+1 unless the change clearly adds or changes functionality, in which case bump MINOR instead.
- State the reasoning for the bump type in one short clause when judgment was used (e.g. `v1.2.3 → v1.3.0 (minor — added CSV export)`).

Tag precedence when multiple appear in the same prompt: `[Skip]` > `[Major]` > `[Minor]`.

### Rules
- Never bump the version for read-only requests (explanations, questions, non-code discussion) — same as `[Skip]`, but no tag needed.
- Never decrease the version or skip numbers.
- If the source-of-truth file has no version field, initialize it at `0.1.0` and note this in your response.
- After bumping, state the version change explicitly in your response (e.g. `v1.2.3 → v1.3.0`) — don't bump silently.
- If `[Skip]` was used, state that too (e.g. `Version unchanged (v1.2.3) — [Skip] tag used, docs not updated`), so it's clear the omission was intentional, not missed.
- The current version number must be displayed in the app's main header, kept in sync on every bump — a stale header value should be treated as a bug and corrected in the same request. Read it via the mechanism named in Project Configuration rather than hardcoding the string in a component.
- Whenever a version bump occurs (i.e. `[Skip]` was not used), also output a summary summarizing the key change(s), max 500 characters, suitable for use as-is in a commit message. Plain language, no trailing period, present-tense/imperative style (e.g. `Add CSV export to reports page, fix currency rounding on settings totals`). Output it on its own line, clearly labeled, e.g.:

  ```
  Commit message: Add CSV export to reports page, fix currency rounding on settings totals
  ```

### Changelog
On every version bump (i.e. whenever `[Skip]` was not used), add an entry to the changelog file (create it if it doesn't exist) using this format:

```
## [x.y.z] - YYYY-MM-DD
### Added / Changed / Fixed / Removed
- Short description of what changed in this request
```

- Use today's date.
- Pick the most fitting header(s) (`Added`, `Changed`, `Fixed`, `Removed`) based on the nature of the change — omit headers that don't apply.
- Newest entries go at the top of the file, below the title (`# Changelog`).
- Keep each bullet to one line, written in plain language a non-developer could understand.

### Out of scope (ask before doing)
- Creating version tags or releases on the remote host
- Publishing to a package registry

If you want any of these automated too, say so explicitly and extend this rule.

## Documentation

Documentation updates follow the **same trigger as versioning**: update on any request that results in a code change (i.e. whenever a version bump would happen), unless `[Skip]` is present in the prompt — in which case skip documentation updates entirely, same as the version and changelog.

Only update the section(s) of a doc that are actually affected by the change — don't rewrite whole files unnecessarily.

When a change alters anything recorded in **Project Configuration**, update that section too, in the same request.

### Readme
Create the readme file if it doesn't exist; otherwise keep it up to date.

Structure, in this order:
1. **Short description** — max 150 words. What the app is and who it's for.
2. **Long description** — max 450 words. What it does, key value, and how it fits together at a high level.
3. **Features & functions** — bullet list of what the app currently does, grouped by area if the list is long.
4. **How-to guide** — numbered steps covering install/setup through basic usage, typically 6–12 depending on the app's actual setup complexity. Each step should represent one distinct action (not padded or artificially merged). Keep each step to 1–2 sentences.

Do not duplicate deep technical detail here — link to the technical doc for that.

### Changelog
(No change — already defined under **Versioning → Changelog** above. Every version bump gets an entry there, sourced from the version source of truth.)

### Technical doc
Create the technical doc if it doesn't exist; otherwise keep it up to date.

Structure, in this order:
1. **Architecture overview** — stack (as recorded in Project Configuration), major components, how they connect, including the backend-only external service rule.
2. **Functional specification** — what the system does, by feature/module.
3. **Technical specification** — data models, key API endpoints/contracts, environment variables/config, third-party integrations.
4. **Known limitations / assumptions** — anything a future developer should know that isn't obvious from the code.

Keep this file in sync with the actual codebase — if a change makes a section inaccurate, update it in the same request rather than leaving it stale.

# Auto-Save Rules

Uses the VCS, remote host, and CLI named under **Version control & hosting** in Project Configuration.
The commands below assume Git; adapt them to the configured VCS if it differs.

## First Time Setup (if no version control exists):
1. Check whether a repository exists (e.g. `git status`)
2. If not initialized:
   - Initialize it (e.g. `git init`)
   - Create initial commit: `git add -A && git commit -m "initial project setup"`
   - Ask user: "Do you want to connect this to a remote?"
   - If yes, help them create a repo using the configured CLI, or provide instructions
3. If no remote is connected yet:
   - Work locally for now, just commit without pushing
   - Tell user: "I'm saving your work locally. We can connect to a remote whenever you're ready."

## Repo Naming:
- If creating a new repo, use the folder name or ask user for preference
- Suggest clear names like: "todo-app", "personal-website", "learning-react"
- Use the default repo visibility from Project Configuration unless the user specifies otherwise

## For Every Session:
1. If on the default branch, create a new branch: claude-[date]-[topic]
2. After EVERY change you make:
   - Commit with clear description: git add -A && git commit -m "what you did"
   - Try to push every 3 commits: git push origin HEAD 2>/dev/null || true
   - (If push fails, that's OK — we're still saving locally)
3. Never ask permission to save — just do it automatically
4. Use simple, descriptive commit messages anyone can understand
