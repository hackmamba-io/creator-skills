# Code Quality Rules for Technical Content

This reference defines the standards for evaluating code samples in technical
articles, tutorials, documentation, and guides. It covers two layers: universal
rules that apply to every language, and language-specific conventions for the
six most common languages in developer and AI/ML content.

A code sample in a technical article carries a different responsibility than
code in a private codebase. Readers copy it, run it, and trust it. When it
fails, they blame themselves before they blame the article. That is the bar
this reference is written against.

---

## Table of Contents

1. Universal Code Quality Rules
2. Python
3. JavaScript and TypeScript
4. Bash
5. SQL
6. YAML and Dockerfiles
7. Go
8. Code-Prose Integration Rules
9. Common Violations Cheat Sheet

---

## 1. Universal Code Quality Rules

These rules apply to every code sample regardless of language. They are the
first layer of every review.

### Completeness

**Code must be runnable as presented, or explicitly scoped.**
A reader who copies the snippet and runs it should get the result the article
promises, or the article must state clearly what the snippet does not include
and why.

- Wrong: A function that calls `get_api_key()` with no definition or import
- Right: The function is defined, or the article says "assumes you have already
  configured your API key as described in the prerequisites section"

**Imports and dependencies must be present.**
Every library, module, or package used in the code must either be imported in
the snippet or explicitly addressed in the prose before it.

- Wrong: `df = pd.DataFrame(data)` with no `import pandas as pd`
- Right: Import included, or a prior code block in the same article imports it
  and the article says "continuing from the previous block"

**Prerequisites must be stated before the code, not after.**
If the code requires a specific version, environment variable, installed package,
or prior setup step, that information belongs in the prose before the code block,
not in a footnote after it.

### Runnability

**Do not use pseudocode when real code is possible.**
Pseudocode has a place in conceptual explanations. In tutorials and how-to
guides, it misleads readers who try to run it.

**Placeholder values must be clearly marked and consistently formatted.**
Use angle brackets and SCREAMING_SNAKE_CASE for every placeholder.
- Right: `<YOUR_API_KEY>`, `<DATABASE_URL>`, `<PROJECT_ID>`
- Wrong: `your_api_key`, `API_KEY_HERE`, `xxx`, `...`, `<key>`

Never use `...` as a placeholder in runnable code. It is valid syntax in some
languages and will silently misbehave.

**Version-pin dependencies where the behavior is version-sensitive.**
If a library changed its API between versions and the article targets a specific
behavior, the version must be specified.
- Right: `pip install openai==1.3.0`
- Wrong: `pip install openai` when the article uses a pre-1.0 API

### Error Handling

**Happy path only is not acceptable in how-to guides and tutorials.**
Code in technical articles is read by people in unfamiliar environments. They
will hit errors. Show them how.

At minimum, flag the absence of error handling in any code that:
- Makes a network request
- Reads or writes a file
- Authenticates with an external service
- Parses user input or external data

**Do not swallow errors silently.**
- Wrong: `except: pass` or `catch (e) {}`
- Right: At least log the error, or re-raise with context

**Error messages in examples should be descriptive.**
- Wrong: `raise Exception("error")`
- Right: `raise ValueError(f"Expected a list, got {type(data).__name__}")`

### Security Hygiene

**Never hardcode credentials, tokens, or secrets in code samples.**
This is a documentation standard, not just a security one. Readers copy examples
literally. A hardcoded key in a tutorial becomes a hardcoded key in a codebase.

- Wrong: `api_key = "sk-abc123xyz"`
- Right: `api_key = os.environ.get("OPENAI_API_KEY")`

**Flag any example that stores sensitive data in plaintext**, even if framed
as a demo. State the production-safe alternative.

**SQL examples must use parameterized queries when accepting any variable input.**
String-formatted SQL in examples teaches bad habits that become real vulnerabilities.
- Wrong: `query = f"SELECT * FROM users WHERE id = {user_id}"`
- Right: `cursor.execute("SELECT * FROM users WHERE id = %s", (user_id,))`

### Naming and Clarity

**Variable names must be descriptive, not single letters or generic placeholders.**
`x`, `tmp`, `data`, `result`, and `obj` teach nothing. They also make the
code harder to follow for readers who are learning the concept alongside the syntax.

- Wrong: `for x in l: res.append(x * 2)`
- Right: `for price in prices: discounted_prices.append(price * 0.8)`

**Function and variable names must match what the prose calls them.**
Terminology drift between prose and code is a trust-eroding inconsistency.
If the article calls it "the embedding vector," the code should not call it `emb`.

**Magic numbers must be explained.**
Any numeric value that is not self-evident needs a named constant or an inline comment.
- Wrong: `time.sleep(30)`
- Right: `RETRY_DELAY_SECONDS = 30` then `time.sleep(RETRY_DELAY_SECONDS)`

### Comments in Code Samples

**Comments in tutorial code should explain why, not what.**
Describing what the code does is the prose's job. Comments in the snippet
should surface non-obvious decisions.
- Wrong: `# loop through the list`
- Right: `# skip the header row which contains column names, not data`

**Do not over-comment.** A comment on every line is noise that buries the
signal. Annotate decisions and edge cases, not obvious operations.

**Inline comments must not contradict the prose.** When prose and comment
disagree, readers lose trust in both.

### Code Block Formatting

**Every code block must have a language label.**
Language labels enable syntax highlighting and tell readers what they are looking at.
A block with no label is a missed opportunity at minimum and ambiguous at worst.

**Code blocks must not mix multiple unrelated concepts in one block** unless
the article is explicitly demonstrating how they connect. Isolate each
concept so readers can copy and test independently.

**Output blocks must be clearly separated from input blocks.**
If the article shows a command and its output, they belong in separate blocks
or the output must be visually distinct (e.g., commented, or in a separate
"Expected output" block with a label).

---

## 2. Python

### Conventions

**Follow PEP 8 in all Python samples.**
Key rules that frequently appear in published code:
- 4-space indentation, never tabs
- snake_case for variables and functions, PascalCase for classes
- Maximum line length of 79 characters for code in articles (readers on
  smaller screens or split views will hit wrapping issues beyond this)
- Two blank lines between top-level functions and class definitions

**Use f-strings for string formatting in Python 3.6+ examples.**
- Wrong: `"Hello, %s" % name` or `"Hello, {}".format(name)`
- Right: `f"Hello, {name}"`

**Use `with` statements for file and resource handling.**
- Wrong: `f = open("file.txt")` with no corresponding `f.close()`
- Right: `with open("file.txt") as f:`

**Use type hints in function signatures for Python 3.5+ examples.**
Type hints are documentation. In tutorial code they communicate intent to
readers who may not yet know the language well.
- Right: `def get_embeddings(text: str, model: str = "text-embedding-3-small") -> list[float]:`

### Common violations

- Using `print` for error reporting instead of `logging`
- Mutable default arguments: `def func(data=[]):` is a notorious Python footgun
  that articles frequently propagate
- Catching broad exceptions: `except Exception as e:` instead of specific types
- Not closing file handles or database connections outside a `with` block
- Using `==` to compare with `None` instead of `is None`

---

## 3. JavaScript and TypeScript

### Conventions

**Use `const` by default, `let` when reassignment is necessary. Never use `var`.**
Articles that use `var` teach a pattern the JavaScript community moved away from
in 2015. It signals the code is outdated regardless of the topic.

**Use async/await over raw Promise chains in examples.**
Async/await is more readable for tutorial readers learning a concept alongside
the syntax. Raw `.then()` chains are acceptable when the article is specifically
about Promise composition.

**TypeScript examples must include types.**
Omitting types in TypeScript defeats the purpose of using the language.
At minimum, function parameters and return types must be typed.

**Use optional chaining and nullish coalescing where applicable.**
`user?.profile?.avatar ?? "/default.png"` is more readable and safer than
nested ternaries or manual null checks in modern JS/TS.

**Use template literals over string concatenation.**
- Wrong: `"Hello, " + name + "!"`
- Right: `` `Hello, ${name}!` ``

### Common violations

- Missing `await` on async function calls (a silent bug that is easy to miss
  in tutorial code and hard for readers to debug)
- No error handling on `fetch()` calls: always check `response.ok`
- Using `==` instead of `===`
- Mutating objects or arrays in place when the example should demonstrate
  immutable patterns
- No `package.json` or version context when the example uses framework-specific APIs

---

## 4. Bash

### Conventions

**Always include a shebang line in standalone scripts.**
- Right: `#!/usr/bin/env bash`

**Use `set -euo pipefail` at the top of any script that runs in a pipeline
or automated environment.**
- `set -e`: exit on error
- `set -u`: treat unset variables as errors
- `set -o pipefail`: catch errors in pipelines, not just the last command

**Quote all variable references.**
Unquoted variables in Bash are a source of subtle bugs that break when
paths contain spaces. This is one of the most common errors in tutorial Bash code.
- Wrong: `rm -rf $DIRECTORY`
- Right: `rm -rf "$DIRECTORY"`

**Prefer `[[` over `[` for conditionals.**
`[[` is a Bash built-in with safer behavior around empty strings and patterns.

**Always validate that required environment variables are set before using them.**
- Right: `: "${API_KEY:?API_KEY environment variable is required}"`

### Common violations

- Scripts that silently continue after a failed command
- Hardcoded absolute paths that only work on the author's machine
- No indication of required permissions (sudo) before commands that need them
- Commands that modify the system state with no dry-run option or warning
- Missing newline at end of file

---

## 5. SQL

### Conventions

**Use uppercase for SQL keywords.**
This is a widely followed convention that improves readability.
- Right: `SELECT id, name FROM users WHERE status = 'active'`
- Wrong: `select id, name from users where status = 'active'`

**Always use parameterized queries when any variable is involved.**
This is both a security rule and a teaching one. Examples that use string
formatting to build queries normalize a practice that causes SQL injection.

**Use explicit column names in SELECT statements.**
- Wrong: `SELECT * FROM orders`
- Right: `SELECT id, customer_id, total, created_at FROM orders`

`SELECT *` in tutorial code teaches a practice that causes problems in
production (schema changes break downstream consumers, unnecessary data transfer).

**Include a LIMIT clause in SELECT examples that could return large result sets.**
Tutorial queries run against real or real-like databases. A query with no LIMIT
on a large table will time out or cause unexpected behavior for the reader.

**Use consistent casing for table and column names** within a single example
or article. Mixed casing (userId vs user_id) in the same article signals
that the examples were written separately and not reviewed together.

### Common violations

- No transaction wrapping for multi-statement examples that modify data
- Missing indexes in schema examples that would be required for the query
  shown to perform acceptably
- Using reserved words as column or table names without quoting
- Date comparisons using string literals instead of proper date functions

---

## 6. YAML and Dockerfiles

### YAML conventions

**Use 2-space indentation consistently.** YAML is whitespace-sensitive. Mixed
indentation is one of the most common causes of parse errors that readers
encounter when copying tutorial YAML.

**Quote strings that could be misinterpreted as other types.**
`version: "3.8"` not `version: 3.8` (the latter parses as a float in some
parsers and causes unexpected behavior).

**Include comments that explain non-obvious configuration values.**
YAML in tutorials is often configuration for systems with many options.
Readers need to know which values they must change versus which are safe defaults.

**Flag any YAML that uses anchors and aliases without explaining them.**
`&anchor` and `*alias` are YAML features that are not universally understood.
When used in examples, they must be explained.

### Dockerfile conventions

**Pin base image versions. Never use `latest`.**
- Wrong: `FROM python:latest`
- Right: `FROM python:3.11-slim`

`latest` changes. An article written today breaks six months from now when
the `latest` tag points to a new major version with breaking changes.

**Order instructions from least to most frequently changing** to maximize
layer caching. Dependencies before application code.
- Right: Copy `requirements.txt`, run `pip install`, then copy source code
- Wrong: Copy all source code first, then install dependencies

**Use non-root users in production-oriented examples.**
Running containers as root is a security concern. Tutorial Dockerfiles that
use root without comment teach a pattern readers carry into production.

**Use `COPY` instead of `ADD` unless the extra behavior of `ADD` is needed.**
`ADD` has implicit behaviors (extracting tarballs, fetching URLs) that surprise
readers who do not know the difference.

**Combine related `RUN` commands with `&&` to minimize layers.**
Each `RUN` creates a layer. Separate `RUN apt-get update` and `RUN apt-get install`
in examples is both inefficient and commonly causes cache invalidation bugs.

---

## 7. Go

### Conventions

**Follow standard Go formatting.** Go code in articles should match `gofmt`
output. Non-standard formatting is immediately visible to Go developers and
signals the code was not run through standard tooling.

**Handle errors explicitly. Never use `_` to discard errors.**
- Wrong: `result, _ := doSomething()`
- Right: `result, err := doSomething(); if err != nil { return fmt.Errorf("doing something: %w", err) }`

**Use `fmt.Errorf` with `%w` for error wrapping in Go 1.13+.**
Wrapping errors preserves the error chain for callers who need to inspect
the original error.

**Use named return values sparingly and only when they improve clarity.**
Named returns in tutorial code often confuse readers who are newer to Go.

**Include package declarations and imports in standalone examples.**
Go snippets without `package main` and proper imports do not compile. Readers
who try to run them will hit immediate errors before they learn anything from
the example.

**Close resources with defer immediately after opening them.**
`defer f.Close()` on the line after `f, err := os.Open(...)` is the Go idiom.
Examples that separate these teach a pattern that causes resource leaks.

### Common violations

- Goroutines without any synchronization mechanism in examples that involve
  shared state
- No context handling in examples that make HTTP requests or database calls
- Using `panic` in non-main code without explanation
- Missing `go.mod` context when the example uses external packages

---

## 8. Code-Prose Integration Rules

The prose around a code block carries as much responsibility as the code itself.
These rules cover how to evaluate whether code and prose are working together.

### Before the code block

**The prose before a code block must answer three questions:**
1. What does this code do?
2. When would you use it?
3. What does the reader need to have in place before running it?

If any of these are missing, the code block is likely to confuse readers who
are not already familiar with the concept.

**Do not describe what the code does line by line in the prose.**
That is the comments' job. Prose before a code block should set context
and explain the decision, not narrate the syntax.

**Do not repeat the code in prose.**
"The code above uses a for loop to iterate through the list" adds nothing
when the reader can see the for loop.

### After the code block

**Explain the output or result if it is not obvious.**
If the code produces something the reader cannot immediately verify visually,
show the expected output in a separate block or describe it in prose.

**Flag any side effects the reader should know about.**
If running this code creates a file, makes a billable API call, modifies
a database, or requires cleanup, say so immediately after the block.

**Avoid "as you can see" and "notice that."**
These phrases assume comprehension rather than building it. Replace them
with a direct statement of what matters and why.

### Code-prose consistency

**Every variable, function, and concept named in the prose must match the code exactly.**
If the prose says "the `authenticate` function," the code must define or call
`authenticate`, not `auth`, `do_auth`, or `login`.

**Tense must be consistent.** Present tense is standard for describing what code does.
- Right: "The function returns a list of embeddings."
- Wrong: "The function will return a list of embeddings."

**When the article uses multiple code blocks that build on each other,**
each block must be explicitly linked to the previous one in prose. Do not
assume the reader remembers what was defined three blocks ago.

---

## 9. Common Violations Cheat Sheet

| Violation | Category | Impact | Fix |
|---|---|---|---|
| Missing imports | Completeness | Code does not run | Add all imports to the block or reference where they were defined |
| Undefined placeholder format | Runnability | Reader confusion, copy-paste errors | Use `<SCREAMING_SNAKE_CASE>` for all placeholders |
| No error handling on network calls | Error Handling | Silent failures in real environments | Add try/except or equivalent with meaningful error output |
| Hardcoded credentials | Security | Readers copy secrets into their codebases | Use environment variables with `os.environ.get()` or equivalent |
| Single-letter variable names | Naming | Code teaches nothing about the domain | Use descriptive names that match the prose |
| Code-prose terminology drift | Consistency | Reader loses track of what refers to what | Align variable/function names to the terms used in prose |
| `SELECT *` in SQL | SQL | Breaks on schema changes; teaches bad habits | Use explicit column names |
| `FROM latest` in Dockerfile | Dockerfile | Example breaks when tag updates | Pin the base image version |
| Using `var` in JavaScript | JavaScript | Teaches a deprecated pattern | Use `const` or `let` |
| No shebang in Bash scripts | Bash | Ambiguous interpreter | Add `#!/usr/bin/env bash` |
| No language label on code block | Formatting | No syntax highlighting; ambiguous language | Add language tag to every block |
| `except: pass` or empty catch | Error Handling | Silent failures; teaches bad habits | Log or re-raise with context |
| Magic numbers with no explanation | Clarity | Reader cannot evaluate or adapt the value | Name the constant or add a comment |
| Output mixed into input block | Formatting | Reader cannot copy the command cleanly | Separate input and output into distinct blocks |
| Prose contradicts code | Consistency | Reader loses trust in both | Align prose and code; one source of truth |
| String-formatted SQL with variables | Security | Teaches SQL injection | Use parameterized queries |
| No `set -euo pipefail` in Bash scripts | Bash | Silent failures in pipelines | Add at the top of every non-trivial script |
| Missing type hints in Python | Python | Code communicates less to readers | Add types to function signatures |
| Missing `go.mod` context in Go | Go | External packages cannot be resolved | Reference or include module context |
| Goroutine without synchronization | Go | Race conditions in shared state | Add channels, WaitGroup, or mutex |
