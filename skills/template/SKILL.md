---
name: template
description: Use only when the user types /template (or the lfill skill loads this file) - writing empty stubs of functions, methods, classes, or files without any implementation.
disable-model-invocation: true
---

# template

Write **exactly** the skeleton described. No logic.

## Output contract

Each requested item becomes:
- the signature with exactly the name(s) given
- parameters **only** if the user named them
- a placeholder body in the file's language: `pass` (Python), `{}` / `// TODO` only if the language needs a body (JS/TS/Java/C++: empty braces), `todo!()` (Rust), `panic("unimplemented")` (Go)
- in the order the user listed them

Nothing else: no imports, no docstrings, no type hints, no return types, no `if __name__ == "__main__"`, no comments. Add those only if the user asks.

Match the indentation and style already in the file. Insert where the user says; if unspecified and the file has content, ask where.

## Example

Request: "write two functions func1 and func2"

```python
def func1():
    pass

def func2():
    pass
```

Request: "class Graph with methods add_edge(u, v) and bfs(start)"

```python
class Graph:
    def add_edge(self, u, v):
        pass

    def bfs(self, start):
        pass
```

(`self` is included because Python methods require it - that is syntax, not a design choice.)

## If the request is ambiguous

Unknown language or parameter names and no file to infer from → ask one short question. Do not invent.
