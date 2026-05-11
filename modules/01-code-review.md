# 🔍 MODULE 1: CODE REVIEW (20 minutes)

> 🧭 Module 1 of 5 · [Workshop index](../README.md) · Next: [Module 2 — Refactoring](./02-refactoring.md)

## What You're Doing

You've just inherited the book app codebase. You've never seen it before. You need to understand:
- What does this code do?
- What problems exist?
- What needs to be fixed before shipping?

**With Copilot CLI**: Let it scan the entire codebase, categorize issues by severity, and give you an action plan in 5 minutes.

---

## Step 1: Run Your First Code Review

**First, start the Copilot CLI by running this one-liner in your terminal:**

```bash
copilot
```

**Then, copy and paste this prompt at the Copilot CLI prompt:**

```bash
> Review @samples/book-app-project/book_app.py for code quality
```

**What happens:**
- Copilot CLI reads the file
- It analyzes the code
- It returns findings organized by category (error handling, input validation, etc.)
- Each finding includes a specific line number and suggestion

**Take 5 minutes**: Read through the output. What issues did it find? Are they critical, or minor style issues?

---

## Step 2: Get a Prioritized Action Plan

Now let's ask for a structured checklist so we know what to tackle first.

**Copy and paste this command:**

```bash
copilot

> Review @samples/book-app-project/ and create a markdown checklist of issues found, 
> categorized by:
> - Critical (data loss risks, crashes)
> - High (bugs, incorrect behavior)
> - Medium (performance, maintainability)
> - Low (style, minor improvements)
```

**What happens:**
- Copilot CLI scans the **entire project** (all files)
- It finds all issues
- It categorizes them by severity
- You get a ready-to-use checklist

**Take 3 minutes**: Look at the checklist. Star the top 3 issues to fix.

---

## Step 3 (Optional): Pro Tip - Using the `/review` Slash Command

<details>
<summary>💡 <b>Optional Pro Tip — click to expand</b>: use the <code>/review</code> slash command for pre-commit reviews</summary>

You've now learned how to review code using **text prompts**. But Copilot CLI also has a **slash command** optimized for a different use case: **reviewing actual changes** you're about to commit.

### The Key Difference

**What you just did (Text Prompt - Step 1 & 2):**
- Scans the entire codebase
- Generates a comprehensive report of all issues
- Best for: Understanding an inherited project

**The Slash Command (`/review`):**
- Analyzes **only your staged/unstaged changes** (git diffs)
- High signal-to-noise output: only shows what **actually changed**
- Best for: Code review before committing/pushing

### When to Use `/review`

`/review` is your tool for **pull request reviews and pre-commit checks**. Here's why it's powerful:

- **Focuses on changes**: Ignores existing code, only reviews your modifications
- **High signal-to-noise**: No noise about code that's been stable for years
- **Pre-commit workflow**: Catch issues before they hit git
- **Pull request reviews**: Analyze exactly what changed in your PR

### Text Prompt vs. Slash Command - Updated Comparison

| Aspect | Text Prompt (`> Review...`) | Slash Command (`/review`) |
|--------|---------------------------|---------------------------|
| **Scope** | Entire project/files | Only staged/unstaged git changes |
| **Signal-to-noise** | Lower (scans all code) | ✅ **High** (only diffs) |
| **Speed** | Slower - full scan | Faster - changes only |
| **Best for** | Onboarding, project audit | Code review, pre-commit checks |
| **Use case** | "Show me everything wrong" | "Review my changes before I commit" |

### Try the Slash Command (Optional)

To see `/review` in action with actual changes:

```bash
cd samples/book-app-project

# Make a small change to a file
echo "# Review test" >> book_app.py

# Then run:
copilot
/review
```

**What you'll see**: Only your modification highlighted for review—not the entire file.

**Key insight**: `/review` gives you **laser-focused feedback** on exactly what you changed, with high-quality analysis and minimal noise.

</details>


---

### 👉 Next up: Module 2 — Refactoring

You've got a prioritized list of what to work on. Next you'll use Copilot — including its Plan Mode — to actually fix the most impactful issues, starting with type hints and input validation.

[**Continue → Module 2 — Refactoring**](./02-refactoring.md)
