# 🚀 MODULE 5: Parallel Analysis with /fleet Mode

> 🧭 Module 5 of 5 · [Workshop index](../README.md) · Previous: [Module 4 — Debugging](./04-debugging.md) · Next: [Wrap-up](./wrap-up.md)

## Why Fleet Mode?

You've now learned workflows sequentially: review → refactor → test → debug. But in real teams, developers work on **multiple independent analyses in parallel**.

Copilot CLI's **fleet mode** (`/fleet`) enables **parallel subagent execution**—multiple independent agents run simultaneously instead of one at a time.

**Example**: Instead of running 3 separate analyses sequentially (15 minutes each = 45 minutes total), you run them all in parallel (~15 minutes total).

---

## Challenge Scenario

Your manager says:

> "We have 3 important analyses for the book-app:
> 1. **Security review** - What vulnerabilities exist?
> 2. **Performance audit** - What's inefficient?  
> 3. **Documentation scan** - What's undocumented?
>
> Run them in parallel with fleet mode. Tell me what you find."

This is a real workflow: teams often analyze code from multiple angles simultaneously.

---

## How `/fleet` Actually Works

`/fleet` is **a single slash command that takes a multi-part prompt**. The main Copilot agent acts as an **orchestrator**: it analyzes your prompt, decomposes it into independent subtasks, and dispatches a subagent for each one. Where the subtasks don't depend on each other, those subagents run **in parallel**.

You don't "enter fleet mode" and then send agents one by one. You write **one** prompt that lists everything you want done, and Copilot figures out what can run in parallel.

> 💡 **Best practice**: Structure your prompt so each work item maps to a **discrete artifact** (a specific file, folder, or concern). The clearer the boundaries, the better the orchestrator parallelizes.

---

---

### Step 1: Launch All 3 Analyses in One `/fleet` Prompt (2 minutes)

**Copy and paste this single prompt at the `>`:**

```
/fleet Run the following three independent analyses on @samples/book-app-project/ in parallel and produce a separate report for each:

1. SECURITY: Analyze the codebase for security vulnerabilities. Look for input validation gaps, unsafe operations, data exposure risks, and injection points.

2. PERFORMANCE: Analyze the codebase for performance issues. Look for inefficient loops, n+1 problems, unnecessary computations, and memory inefficiencies.

3. DOCUMENTATION: Review the codebase for documentation quality. Check for missing docstrings, unclear comments, undocumented parameters, and missing type hints.

Return three clearly-labeled sections — Security, Performance, Documentation — each with prioritized findings.
```

**What happens**:
- Copilot's orchestrator reads the prompt and identifies 3 independent subtasks.
- It spawns **3 subagents**, one per analysis, each with its own context window.
- Because the analyses don't depend on each other, the subagents run **in parallel**.
- You only had to send one message — the orchestrator did the splitting for you.

---

### Step 2: Monitor Progress (5 minutes)

**At the `>` prompt, type:**

```
/tasks
```

**What you'll see**:
- A list of background subtasks created by `/fleet`.
- Status for each subagent (running / completed).
- Use ↑/↓ to navigate, Enter to view details, `r` to remove finished tasks, Esc to exit.

**Key insight**: All 3 subagents are working **at the same time**, each in its own context window. If you'd asked the same questions one-by-one in a normal session, you'd wait for each to finish before starting the next.

---

### Step 3: Review Results & Reflect (7 minutes)

When all 3 subagents complete, the orchestrator combines their reports into a single response.

1. **Review Security Findings**: What vulnerabilities did it find?
2. **Review Performance Findings**: What inefficiencies exist?
3. **Review Documentation Findings**: What's missing?

**Compare them**:
- Are findings clearly different? (Security ≠ Performance ≠ Documentation)
- Did each subagent stay focused on its assigned concern?
- Are the results actionable?

**Reflect on efficiency**:

| Approach | Time |
|---|---|
| Sequential (3 prompts, one after the other) | ~3× the longest single analysis |
| Parallel via `/fleet` (one combined prompt) | ~1× the longest single analysis |

For larger codebases or more analyses, the savings multiply.

> ⚡ **Pro tip**: For complex multi-step changes, build an implementation plan first (press **Shift+Tab** to enter plan mode), then choose **"Accept plan and build on autopilot + /fleet"** to let Copilot execute the whole plan with subagents in parallel.

---

## 🎼 Optional Exercise: Orchestrate All Four Workflows with One `/fleet` Prompt

If you finished Module 5 with time to spare, here's a stretch exercise. **Rethink Modules 1–4 as parallel work.**

In Modules 1–4 you ran each workflow **sequentially on the same module**: review → refactor → test → debug, where each step depended on the previous one. That made sense — you were building understanding step by step.

But in a real team, those same four skills are often applied **in parallel to different parts of the codebase** by different people. Code review on one module, debugging on another, refactoring on a third, test generation on a fourth — all happening at once.

In this stretch exercise you'll do exactly that: take the four workflows you just learned (review, debug, refactor, test) and dispatch them as **one `/fleet` prompt** that targets four discrete artifacts. The orchestrator will run all four subagents in parallel.

> 💡 **Why it works**: each workstream targets a **different file or folder** with **no dependencies** on the others — exactly the conditions `/fleet` needs to parallelize.

<details>
<summary>🚀 <b>Click to expand the stretch exercise: Parallel Task Streams with /fleet</b></summary>

## From Analysis to Complete Workflows

The basic Module 5 challenge showed you how /fleet handles **independent analyses** (security, performance, documentation) running in parallel.

But /fleet is more powerful: it can handle **complete development workflows**—all four skills (review, refactor, debug, test) working in parallel across **different task types**.

This is how professional development teams actually operate.

---

## Real-World Scenario

Your engineering lead says:

> "We have parallel workstreams on the book-app. I need four things happening simultaneously:
>
> 1. **QA Lead**: Audit the code quality of the entire app. What issues exist?
> 2. **Debugging Specialist**: We have a critical bug—when marking one book as read, ALL books get marked. Root-cause it and suggest a fix.
> 3. **Architecture Lead**: Refactor the main CLI handler. Add type hints, improve command routing, enhance error handling.
> 4. **Test Lead**: Generate comprehensive tests for all book operations and command handlers.
>
> Use `/fleet` to dispatch them all from one prompt. Report back in 20 minutes."

This scenario exercises **all four of the workflows you've learned** (review, debug, refactor, test), but distributed across **independent parallel tasks** instead of sequential steps on a single module.

---

## Why This Works for /fleet

✅ **Task Independence**: Code review doesn't depend on the bug fix; refactoring doesn't require the tests first  
✅ **Team Specialization**: Different roles (QA, debugging, architecture, testing) work in their areas  
✅ **All Four Workflows**: You use review, debug, refactor, and test—but not on the same object  
✅ **Realistic Pattern**: Enterprise teams work exactly this way  
✅ **Efficiency**: 4 sequential workstreams (~1 hour) → 4 parallel streams (~20 minutes)  

---

## 🧩 Challenge: Try It Yourself (20 minutes)

Now it's your turn. You're the project coordinator. Brief the orchestrator with **one well-structured `/fleet` prompt** and let it dispatch four parallel subagents.

### Setup (3 minutes)

**Scenario** — same as the Real-World Scenario above:
- The **book-app** is your codebase.
- You're deploying a new version Friday.
- QA needs a baseline of issues.
- There's a reported bug (mark-as-read behavior).
- Architecture needs improvement before production.
- Test coverage is critical.

Each work item targets a **discrete artifact** (a specific file or folder), so the orchestrator can parallelize them cleanly.

**Start Copilot CLI:**

```bash
copilot
```

> 💡 **Pro workflow** (optional): Press **Shift+Tab** to enter plan mode, draft an implementation plan together with Copilot, then choose **"Accept plan and build on autopilot + /fleet"** to let Copilot execute the whole plan with subagents in parallel. For this exercise we'll use `/fleet` directly.

---

### 🐛 Your Mission (17 minutes)

Write **one** `/fleet` prompt that launches these four independent workstreams in parallel and asks for a clearly-labeled report from each:

| # | Workstream | Target file / folder | Goal |
|---|---|---|---|
| 1 | **Code Quality Audit** | `@samples/book-app-project/` | Prioritized list of quality issues with HIGH/MEDIUM/LOW severity |
| 2 | **Critical Bug** | `@samples/book-app-buggy/books_buggy.py` | Root cause of "marking one book as read marks ALL books as read", with fix |
| 3 | **Architecture Refactor** | `@samples/book-app-project/book_app.py` | Replace if/elif chain with dictionary dispatch, add type hints, improve error handling |
| 4 | **Test Generation** | `@samples/book-app-project/` | Comprehensive pytest suite covering operations, edge cases, error scenarios |

Then:
1. Submit your prompt at the `>` prompt.
2. Use `/tasks` to monitor the four subagents (↑/↓ to navigate, Enter for details, Esc to exit).
3. When everything finishes, review the four reports and look for **cross-cutting findings** — e.g. did the Audit flag the same root cause the Debug agent isolated? Do the generated tests cover it?

**Take 4–5 minutes** to craft the prompt before peeking at the solution. Be explicit that the workstreams are independent so the orchestrator parallelizes cleanly.

> 💡 **Hints**:
> - Reference each file/folder with `@path` so subagents have scoped context.
> - State the deliverable for each workstream (a list, a root-cause explanation, a refactored snippet, a test suite).
> - End with a sentence like "These workstreams are independent — run them in parallel."

<details>
<summary>✅ <b>Click to reveal a working solution</b> (try it yourself first!)</summary>

**Example `/fleet` prompt:**

```
/fleet Run the following four independent workstreams in parallel and return a clearly-labeled report for each:

1. CODE QUALITY AUDIT (review) — on @samples/book-app-project/
   Audit the entire codebase for quality issues: naming, complexity, structure, missing type hints, input validation gaps, error handling problems, and unhandled edge cases. Return a prioritized list with severity (HIGH/MEDIUM/LOW).

2. CRITICAL BUG (debug) — on @samples/book-app-buggy/books_buggy.py
   A reported bug: "When marking one book as read, ALL books get marked as read." Identify the root cause, show the specific lines, explain why it happens, suggest a fix, and describe user impact.

3. ARCHITECTURE REFACTOR (refactor) — on @samples/book-app-project/book_app.py
   Refactor command handling for production quality: replace the if/elif chain with a dictionary dispatch pattern, add complete type hints, improve error handling, and suggest one architectural improvement for maintainability.

4. TEST GENERATION (test) — on @samples/book-app-project/
   Generate a comprehensive pytest suite covering all book operations (add_book, show_books, mark_as_read, get_books), edge cases (empty title/author, invalid years like -5000 or 99999, no books), happy paths for all command handlers, error scenarios, and expected output formats.

These four workstreams are independent — they target different files and concerns, so they should run in parallel.
```

**What happens**:
- The orchestrator analyzes your prompt and identifies 4 independent workstreams.
- It spawns **4 subagents**, each with its own context window, scoped to its assigned artifact.
- Because the workstreams target different files and don't depend on each other, the subagents run **in parallel**.
- You sent **one** prompt — the orchestrator handled the splitting.

**Suggested review order once `/tasks` shows everything complete:**

1. **Code Quality Audit** — What quality issues exist? Which are HIGH priority? Which align with what the Debug subagent found?
2. **Critical Bug** — What's the root cause? Does it match anything the Audit flagged? How would the Refactor's changes prevent it?
3. **Architecture Refactor** — What did it propose? Does it address the Audit's issues? Would it prevent bugs like the one the Debug subagent found?
4. **Test Generation** — Do the tests cover what the Audit and Debug subagents identified? Are edge cases covered? Would these tests catch the mark-as-read bug?

**Synthesis**: Notice how all four subagents contributed different perspectives on the *same codebase* — the Audit found issues; Test Generation wrote tests for them; Debug isolated a specific bug; Refactor's changes could prevent similar issues. All happened simultaneously, from a single prompt.

</details>

---

</details>

---


---

### 👉 Next up: Wrap-up

You've seen the whole loop, including how to parallelize it. The wrap-up collects the key takeaways and points you at the prompt cheat sheet.

[**Continue → Wrap-up**](./wrap-up.md)
