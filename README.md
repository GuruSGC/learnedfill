# learnedfill

A coding-agent skill set for people who want to stay in charge of their own code.

Instead of letting an agent generate hundreds of lines, **learnedfill** only writes the lines you already know you want. The agent saves you typing; the design and logic stay your responsibility.

## Commands

| Command | What it does |
|---|---|
| `/lfill <request>` | Main entry. Decides whether the request is a layout or functionality, announces the pick (`lfill → /template` or `lfill → /lfunc`), then runs it. |
| `/template <request>` | Writes only skeletons: signatures with the exact names given and empty bodies (`pass`). No imports, docstrings, or logic. |
| `/lfunc <request>` | Writes functionality exactly the way you want it. Asks numbered question rounds (scope, approach, edge cases) with a recommended answer for each, waits for your go, then writes only the confirmed part. |

All three run **only** when typed explicitly; the agent never triggers them on its own.

## Examples

```
/lfill write two functions func1 and func2
```
```python
def func1():
    pass

def func2():
    pass
```

```
/lfill in lcs.py add a 2d array dp
```
→ asks how big, how to build it, and whether you want just the declaration or the loops too, then writes only what you confirm.

## Install

**Claude Code (manual):**

```bash
git clone https://github.com/GuruSGC/learnedfill
cp -r learnedfill/skills/* ~/.claude/skills/
```

**Via skills.sh:**

```bash
npx skills add GuruSGC/learnedfill
```

Restart your session after installing so the commands are picked up.

## Structure

```
skills/
  lfill/SKILL.md        router
  template/SKILL.md     stubs only
  lfunc/SKILL.md        functionality
  lfunc/writer.md       how lfunc clarifies, suggests, and writes
  lfunc/sources/        upstream skills writer.md is adapted from
```

## Credits

`writer.md` adapts ideas from two MIT-licensed skills (originals kept in `skills/lfunc/sources/`):

- [grilling](https://github.com/mattpocock/skills) by Matt Pocock: question rounds with recommended answers
- [karpathy-guidelines](https://github.com/multica-ai/andrej-karpathy-skills): think before coding, simplicity first, surgical changes

## License

MIT
