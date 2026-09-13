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

```
/lfill stub a class Stack with push, pop, peek and implement push using a python list
```
→ writes the three method stubs, then asks where the list should live, what the parameter is called, and which end is the top before writing only `push`.

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
  lfill/SKILL.md                  router
  template/SKILL.md               stubs only
  lfunc/SKILL.md                  functionality
  lfunc/writer.md                 how lfunc clarifies, suggests, and writes
  lfunc/sources/                  upstream skills writer.md is adapted from
  lfunc/THIRD_PARTY_NOTICES.md    licenses for lfunc/sources/
  */LICENSE                       MIT license, copied into each skill so it travels with installs
```

## Troubleshooting

| Problem | Fix |
|---|---|
| `/lfill` (or `/template`, `/lfunc`) is not recognized | Check each folder landed at `~/.claude/skills/<name>/SKILL.md` (not nested one level deeper), then restart the session. |
| `/lfill` announces a pick but can't load the sub-skill | All three folders must be installed side by side in the same skills directory. Install all of them, not just `lfill`. |
| It picked `/template` when you wanted code (or vice versa) | Say so - it switches without argument. Or call `/template` or `/lfunc` directly. |
| `/lfunc` asks questions when you already know exactly what you want | Give the exact line or approach in the request (e.g. `add dp = [[0]*(m+1) for _ in range(n+1)]`) and it writes it directly. |
| The skills start on their own | They shouldn't. Check each `SKILL.md` still has `disable-model-invocation: true` in its frontmatter. |

## Privacy

learnedfill is plain Markdown instructions. It contains no scripts, makes no network requests or API calls, and collects, stores, or transmits no data.

## Support

Questions, bugs, and security concerns: open an issue at [github.com/GuruSGC/learnedfill/issues](https://github.com/GuruSGC/learnedfill/issues). Maintainer: [@GuruSGC](https://github.com/GuruSGC).

## Credits

`lfunc/writer.md` is built on two MIT-licensed skills. Thanks to their creators:

- **[grilling](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling)** by **Matt Pocock** ([@mattpocock](https://github.com/mattpocock)): the question-round format with a recommended answer for each question.
- **[karpathy-guidelines](https://github.com/multica-ai/andrej-karpathy-skills)** by **Jiayuan Zhang** ([@forrestchang](https://github.com/forrestchang)), based on observations by **Andrej Karpathy** ([@karpathy](https://github.com/karpathy)): think before coding, simplicity first, surgical changes.

The original files are kept unmodified in `skills/lfunc/sources/`.

## License

MIT - see [LICENSE](LICENSE). Third-party files keep their own MIT licenses - see [skills/lfunc/THIRD_PARTY_NOTICES.md](skills/lfunc/THIRD_PARTY_NOTICES.md).

This project is not affiliated with or endorsed by Anthropic, Matt Pocock, Jiayuan Zhang, or Andrej Karpathy.
