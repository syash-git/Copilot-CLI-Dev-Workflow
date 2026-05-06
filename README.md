# Development workflows with Copilot-CLI

> **Welcome! In the next 45-60 minutes, you'll learn five essential development modules using Copilot CLI. Don't just learn about them—*do* them, right now, on your laptop.**

---

## 📖 The Story

It's your first week on a new team. Your team lead points you at a small project — the **book app**, a Python CLI that manages a book collection. The code works, but it hasn't been reviewed, tested, or hardened, and the team would like it cleaned up before it ships.

Your lead suggests a way to get through it quickly:

> *"Use the Copilot CLI. Treat it like a pair programmer — it can review code, suggest refactors, generate tests, and help you debug. We'll walk through the same four workflows we use on real work every day, plus a parallel mode for tackling several at once."*

Open your terminal and the workshop guide — that's what the rest of this repo is for.

---

## ✅ BEFORE YOU START

Make sure you have:

- [ ] **GitHub Copilot CLI installed**: Run `copilot --version`
- [ ] **Python 3.10+**: Run `python --version`
- [ ] **This repository cloned**: `git clone https://github.com/github/copilot-cli-for-beginners`
- [ ] **Terminal open** in the repo directory: `cd copilot-cli-for-beginners`

**Stuck?** See the [Troubleshooting guide](./TROUBLESHOOTING.md).

---

## 📂 What's in this Repo

| File / Folder | What it's for |
|---|---|
| **[`WORKSHOP.md`](./WORKSHOP.md)** | The 45–60 min hands-on workshop — 5 modules covering code review, refactoring, testing, debugging, and parallel `/fleet` analysis. **Start here once you've finished setup.** |
| **[`samples/`](./samples)** | The practice codebases the workshop edits. `book-app-project/` is the clean version; `book-app-buggy/` is the intentionally broken version used in the debugging module. |
| **[`QUICK-REFERENCE.md`](./QUICK-REFERENCE.md)** | Reusable Copilot CLI prompt templates (review, refactor, tests, debug, plan mode) — keep this open after the workshop to apply the same patterns to your own code. |
| **[`TROUBLESHOOTING.md`](./TROUBLESHOOTING.md)** | Fixes for common setup snags: `copilot` not found, auth failures, missing Python, pytest, etc. |

---

## ▶️ Ready?

Open **[WORKSHOP.md](./WORKSHOP.md)** and let's go.

---