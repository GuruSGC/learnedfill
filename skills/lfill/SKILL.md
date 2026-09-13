---
name: lfill
description: learnedfill - use only when the user types /lfill. The user owns the design and logic; the agent is a typing aid that writes only the lines the user already knows they want.
disable-model-invocation: true
---

# learnedfill (/lfill)

**Core rule: write the most minimal set of lines the user asked for. Nothing more.**
The agent saves typing time. It does not build the app, design the logic, or fill gaps with its own ideas. Those are the user's responsibility.

## Routing

Read the request and decide which sub-skill fits:

| The request is about... | Route to |
|---|---|
| Layout / skeletons: "write functions f1 and f2", "stub a class Foo with methods a, b", signatures, empty bodies | `template` |
| Behavior: what code *does* - logic, data structures, algorithms, a line inside a function (e.g. "add a 2d dp array") | `lfunc` |
| Both (e.g. "stub 3 functions and implement the first") | `template` first, then `lfunc` for only the part asked to be implemented |
| Unclear | Ask the user which one. Do not guess. |

## Announce, then load

Before loading, state the pick in one line:

> `lfill → /template` (layout only: 2 function stubs)

or

> `lfill → /lfunc` (functionality: body of `func1`)

Then use the Read tool to load that sub-skill's file and follow it exactly. The sub-skills are locked to explicit slash commands, so the Skill tool cannot load them. They live next to this skill's base directory:
- template → `<this skill's base directory>/../template/SKILL.md`
- lfunc → `<this skill's base directory>/../lfunc/SKILL.md`

If the user says the pick is wrong, switch to the other skill without argument.

## Red flags - stop

- About to write a line the user didn't ask for (imports, helpers, docstrings, error handling, tests, `main`)
- About to "finish" a function the user only asked to stub
- About to pick an implementation approach the user didn't choose
