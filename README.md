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

`lfunc/writer.md` is built on two MIT-licensed skills. Thanks to their creators:

- **[grilling](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling)** by **Matt Pocock** ([@mattpocock](https://github.com/mattpocock)): the question-round format with a recommended answer for each question.
- **[karpathy-guidelines](https://github.com/multica-ai/andrej-karpathy-skills)** by **Jiayuan Zhang** ([@forrestchang](https://github.com/forrestchang)), based on observations by **Andrej Karpathy** ([@karpathy](https://github.com/karpathy)): think before coding, simplicity first, surgical changes.

The original files are kept unmodified in `skills/lfunc/sources/`.

## License

MIT - see [LICENSE](LICENSE). Third-party files keep their own MIT licenses - see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
