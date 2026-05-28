# Development workflows with Copilot-CLI

> **Welcome! In the next 45-60 minutes, you'll learn five essential development modules using Copilot CLI. Don't just learn about them—*do* them, right now, on your laptop.**

---

## 📖 The Story

It's your first week on a new team. Your team lead points you at a small project — the **book app**, a Python CLI that manages a book collection. The code works, but it hasn't been reviewed, tested, or hardened, and the team would like it cleaned up before it ships.

Your lead suggests a way to get through it quickly:

> *"Use the Copilot CLI. Treat it like a pair programmer — it can review code, suggest refactors, generate tests, and help you debug. We'll walk through the same four workflows we use on real work every day, plus a parallel mode for tackling several at once."*

---

## ✅ Before You Start

Make sure you have:

- [ ] **GitHub Copilot CLI installed**: Run `copilot --version`
- [ ] **Python 3.10+**: Run `python --version`
- [ ] **This repository cloned**: `git clone https://github.com/syash-git/Copilot-CLI-Dev-Workflow.git`
- [ ] **Terminal open** in the repo directory: `cd Copilot-CLI-Dev-Workflow`

**Stuck?** See the [Troubleshooting guide](./TROUBLESHOOTING.md).

> 💡 The practice codebase lives in [`samples/book-app-project/`](./samples/book-app-project) — a small Python CLI for managing a book collection. Try it now:
>
> ```bash
> cd samples/book-app-project
> python book_app.py list
> python book_app.py help
> ```

---

## 🧑‍💻 The Workshop

You'll walk through the same loop a developer runs on real work: **review** an inherited codebase (Module 1), **refactor** the issues it surfaces (Module 2), **generate tests** to lock the behaviour in (Module 3), and **debug** what's still broken (Module 4) — then in Module 5 you'll use `/fleet` to run all four in parallel, the way a senior engineer juggles multiple workstreams. Each module pairs a guided walkthrough with a try-it-yourself exercise, so by the end you'll have a repeatable Copilot CLI workflow you can apply to any codebase tomorrow.

### 🗺️ Modules

Work through them in order — each one builds on the last.

1. 🔍 **[Module 1 — Code Review](./modules/01-code-review.md)** · 10 min
   Audit an inherited codebase with Copilot and produce a prioritized fix list.
2. 🛠️ **[Module 2 — Refactoring](./modules/02-refactoring.md)** · 12 min
   Apply the top fixes with Copilot, using **Plan Mode** for the bigger ones.
3. 🧪 **[Module 3 — Test Generation](./modules/03-test-generation.md)** · 10 min
   Lock the behaviour in with a comprehensive pytest suite.
4. 🐛 **[Module 4 — Debugging](./modules/04-debugging.md)** · 12 min
   Reproduce and root-cause two real bugs in the buggy variant of the app.
5. 🚀 **[Module 5 — Parallel Analysis with /fleet](./modules/05-fleet-mode.md)** · 15 min
   Run several of the workflows above in parallel, the way a senior engineer juggles multiple workstreams.

When you finish, head to the **[Wrap-up](./modules/wrap-up.md)** for the key takeaways and a pointer to the prompt cheat sheet.

---

## 📂 What Else is in this Repo

| File / Folder | What it's for |
|---|---|
| **[`modules/`](./modules)** | The five module files plus the wrap-up — linked from the list above. |
| **[`samples/`](./samples)** | The practice codebases the workshop edits. `book-app-project/` is the clean version; `book-app-buggy/` is the intentionally broken version used in the debugging module. |
| **[`QUICK-REFERENCE.md`](./QUICK-REFERENCE.md)** | Reusable Copilot CLI prompt templates (review, refactor, tests, debug, plan mode) — keep this open after the workshop to apply the same patterns to your own code. |
| **[`CHEATSHEET.md`](./CHEATSHEET.md)** | The CLI itself at a glance: slash commands, keyboard shortcuts, mention prefixes (`@`/`#`/`!`), and modes. |
| **[`TROUBLESHOOTING.md`](./TROUBLESHOOTING.md)** | Fixes for common setup snags: `copilot` not found, auth failures, missing Python, pytest, etc. |

---

## 🚦 Ready?

Open **[Module 1 — Code Review](./modules/01-code-review.md)** and let's go.