# 🧑‍💻 The Workshop: Development Workflows with Copilot CLI

> 45–60 minutes • 5 hands-on modules • You'll *do* every workflow on your laptop, not just read about it.

New here? Start with the [README](./README.md) for the story and setup checklist, then come back.

---
# 🔍 MODULE 1: CODE REVIEW (20 minutes)

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

## ✨ Key Insight: Code Review

> You don't just understand the code now—you have a **prioritized action plan**. Instead of guessing what to fix, you know exactly what matters most.

**Remember this**: The workflow is **Understand → Prioritize → Act**. Every time you inherit code, this is your first step.

---

---

# 🛠️ MODULE 2: REFACTORING (15 minutes)

## What You're Doing

You've reviewed the code and found issues. Now it's time to **improve it safely**. Refactoring means changing the structure/organization without breaking functionality.

From the code review, you found **12 HIGH priority issues**:
- **7 Missing type hints** ← We'll fix these first (quick wins, foundational)
- **5 Input validation gaps** ← We'll fix these second (practical bug prevention)
- (Bonus: Architectural improvements like if/elif chains, if time permits)

---

## Step 1: Add Type Hints (HIGH Priority)

Good Python code uses **type hints**—they tell other developers (and tools) what types your functions expect and return. Let's add them to book_app.py.

**Copy and paste this command:**

```bash
copilot

> Review @samples/book-app-project/book_app.py and add complete type hints 
> to all functions. Add parameter types (e.g., books: List[Book]) and 
> return types (e.g., -> None). Import List from typing.
```

**What happens:**
- Copilot scans the file
- It identifies all 7 functions missing type hints
- It suggests adding types like `def show_books(books: List[Book]) -> None:`
- It might even provide the complete refactored code

**Take 5 minutes**: Read the suggestions. Notice how type hints make code clearer? Could a new developer understand what each function expects?

**Example of what Copilot suggests:**
```python
# Before:
def show_books(books):
    ...

# After:
from typing import List

def show_books(books: List[Book]) -> None:
    """Display books in a user-friendly format."""
    if not books:
        print("No books found.")
        return
    # ...
```

---

## 🧠 Quick Primer: Plan Mode (1 minute)

Dont want copilot to make code changes directly? meet **Plan Mode** — it asks Copilot to *think before it types*. Instead of jumping straight to edits, Copilot drafts a step-by-step plan you can review, tweak, or reject. Perfect for multi-step changes like the exercise below.

**How to use it:** type `/plan` inside the Copilot CLI, then describe your goal. Copilot outlines its approach and waits for your approval before changing any code.

```bash
> /plan add input validation to handle_add() in @samples/book-app-project/book_app.py
```

Try it on the next exercise — review the plan, then say "go" to execute.

---

## 🧩 Step 2: Exercise — Improve Input Validation (HIGH Priority)

Time to practice on your own! This is a HIGH priority issue you'll fix yourself with Copilot CLI.

### 🐛 The Challenge

Open `samples/book-app-project/book_app.py` and look at the `handle_add()` function. It has a sneaky bug: **it trusts the user completely**.

Try running the app and adding a book with:
- An **empty title** (just press Enter)
- An **empty author** (just press Enter)
- A year of **`-500`**, **`99999`**, or **`abc123`**

What happens? You'll discover the app happily accepts garbage data — empty strings get stored as "books," and unreasonable years (like year 99999) sail through without complaint. Over time, this corrupts your library file with invalid entries.

**Your mission:**
1. Identify what bad inputs could break this app.
2. Use Copilot CLI to add proper input validation to `handle_add()`.
3. Verify the fix by trying the same bad inputs again.

**Validation requirements:**
- ❌ Reject empty `title` and `author` (after stripping whitespace).
- ❌ Reject years outside the range **1000–2100**.
- ❌ Reject non-numeric year input with a clear message.
- ✅ Show a friendly error message for each failure and return early (don't add the book).

**Take 4 minutes**: Craft your own prompt to Copilot CLI to fix this. Think about what context Copilot needs (the file, the function, the rules).

> 💡 **Hint**: Try starting with `/plan` (see the primer above) so Copilot proposes an approach before editing. Reference the file with `@samples/book-app-project/book_app.py` and be specific about *which* function to change and *what* rules to enforce.

<details>
<summary>✅ <b>Click to reveal the solution</b> (try it yourself first!)</summary>

**Example prompt — using Plan Mode:**

```bash
copilot

# Step A — ask Copilot to draft a plan first
> /plan Improve input validation in handle_add() in 
> @samples/book-app-project/book_app.py. Rules:
> - Reject empty title and author (after stripping whitespace)
> - Restrict year to the range 1000–2100
> - Reject non-numeric year input
> - Show a friendly error and return early on each failure

# Step B — review the plan, then approve to execute
> Looks good — go ahead and apply it.
```

> 💡 If something in the plan looks off, push back instead of approving:
> *"Also handle the case where year input is empty — treat it as invalid."*
> Copilot will revise the plan, then wait for approval again.

**What Copilot does:**
- **Plan phase:** drafts a step-by-step plan (which checks to add, in what order, what messages to print) and waits for your approval — no code changes yet.
- **Execute phase:** once you approve, it edits `handle_add()` to match the plan with proper error handling and user-friendly messages.

**Example before/after:**

```python
# Before:
def handle_add():
    print("\nAdd a New Book\n")
    title = input("Title: ").strip()
    author = input("Author: ").strip()
    # No validation—user could enter empty strings!
    year_str = input("Year: ").strip()
    try:
        year = int(year_str) if year_str else 0
        collection.add_book(title, author, year)
        print("\nBook added successfully.\n")
    except ValueError as e:
        print(f"\nError: {e}\n")

# After:
def handle_add():
    print("\nAdd a New Book\n")
    title = input("Title: ").strip()
    if not title:
        print("\nError: Title cannot be empty.\n")
        return
    
    author = input("Author: ").strip()
    if not author:
        print("\nError: Author cannot be empty.\n")
        return
    
    year_str = input("Year: ").strip()
    try:
        year = int(year_str)
        if year < 1000 or year > 2100:
            print("\nError: Year must be between 1000 and 2100.\n")
            return
        collection.add_book(title, author, year)
        print("\nBook added successfully.\n")
    except ValueError:
        print("\nError: Year must be a valid number.\n")
```

</details>

---

## ✨ Key Insight: Refactoring

> Refactoring isn't random "make it prettier" work. It's **strategic improvement**. Start with **HIGH priority issues** (bugs, missing safety checks), then move to **MEDIUM priority issues** (architectural improvements).
> 
> **Priority pyramid:**
> 1. **HIGH**: Bugs and data quality (type hints, validation) ← Do these first
> 2. **MEDIUM**: Maintainability and extensibility (patterns) ← Do these if time permits
> 3. **LOW**: Style and polish ← Optional

**Remember this**: Always refactor **with tests as your safety net**. That's our next workflow.

---

---

# 🧪 MODULE 3: TEST GENERATION (12 minutes)

## What You're Doing

You've refactored the code. But did you break anything? How confident are you that it still works?

**Without AI**: Manually write 5-10 tests. Probably miss edge cases. Hope nothing breaks.

**With Copilot CLI**: Generate 15-20+ tests automatically, including edge cases you wouldn't think of.

---

## Step 1: Generate Comprehensive Tests

**Copy and paste this command:**

```bash
copilot

> @samples/book-app-project/books.py 
> Generate comprehensive pytest tests. Include tests for:
> - Adding books
> - Removing books
> - Finding by title
> - Finding by author
> - Marking as read
> - Edge cases (empty data, special characters, duplicate entries)
> - Error cases (missing files, corrupted data)
```

**What happens:**
- Copilot CLI analyzes the BookCollection class
- It generates 15-20+ test functions
- Tests cover happy path, edge cases, and error cases
- Each test is runnable, with assertions

**Take 5 minutes**: Look at the generated tests. How many tests were there? Did you spot any testing patterns you didn't expect?

---

## Step 2: Run the Tests

Let's verify those tests actually work.

**In your terminal:**

```bash
cd samples/book-app-project
python -m pytest tests/ -v
```

**What happens:**
- pytest runs all tests
- You see which tests pass/fail
- Green checkmarks = confidence that code works

**Expected result**: All tests pass ✓ (or mostly pass).

**Take 3 minutes**: Watch the tests run. Notice how many tests there are. Could you have written all these manually?

---

## Step 3: Understand What Tests Do

Tests are your safety net. When you refactored earlier, tests would have caught any breaking changes.

**Example test structure you should see:**

```python
# Happy path - normal usage
def test_add_book_creates_book():
    collection = BookCollection()
    collection.add_book("1984", "George Orwell", 1949)
    assert len(collection.list_books()) == 1

# Edge case - empty data
def test_add_book_with_empty_title():
    collection = BookCollection()
    with pytest.raises(ValueError):
        collection.add_book("", "Author", 2020)

# Error case - file doesn't exist
def test_load_books_handles_missing_file():
    collection = BookCollection()
    # Should gracefully handle missing data.json
    assert collection.list_books() == []
```

---

## ✨ Key Insight: Test Generation

> Tests aren't about passing a test suite. They're about **confidence**. When all tests pass, you can ship code fearlessly. When they fail, you know exactly what broke.

**Remember this**: 
- Comprehensive tests = confidence to refactor
- Passing tests = proof that code works
- Failing tests = early warning of problems

---

---

# 🐛 MODULE 4: DEBUGGING (13 minutes)

## What You're Doing

It's late morning. QA sends you a Slack message:

> *"Bug found: When I mark one book as read, ALL books get marked. This breaks everything. Please fix ASAP."*

You're panicking. But instead, you use Copilot CLI to **trace the bug, find the root cause, and fix it surgically**. All before lunch.

---

## Important: We're Switching to the Buggy App

For debugging practice, we're going to use a version of the app that has **intentional bugs**. This lets you see real debugging in action.

---

## Step 1: Reproduce and Debug Bug #1

**The symptom:** When marking one book as read, all books get marked.

**Copy and paste this command:**

```bash
copilot

> @samples/book-app-buggy/books_buggy.py 
> When I mark one book as read, ALL books get marked. Debug why.
```

**What happens:**
- Copilot CLI reads the buggy code
- It traces through the logic
- It finds the exact line where the bug is
- It explains what's wrong
- It shows you the fix

**Expected output structure:**
```
Root Cause (Line 58-65):
The mark_as_read() function doesn't have a condition to check 
if this is the correct book. It marks ALL books as read.

Current code:
for book in self.books:
    book.read = True  # BUG: Sets ALL books to read!

Should be:
for book in self.books:
    if book.title.lower() == title.lower():
        book.read = True  # Only sets matching book
```

**Take 3 minutes**: Read the diagnosis. Does the explanation make sense? Would you have spotted this bug by reading the code?

---

## 🧩 Step 2: Exercise — Debug Bug #2

Great! You fixed the first bug. But there might be more — and this time, **you're the detective**.

### 🐛 The Challenge

**The symptom:** When I try to remove the book "Dune", it also removes "Dune Messiah".

That's a pretty alarming bug. Asking the app to delete one book and losing two is the kind of issue that destroys user trust (and data!).

**Your mission:**
1. Reproduce the bug if you can — add both "Dune" and "Dune Messiah" to `samples/book-app-buggy/books_buggy.py`, then try removing just "Dune".
2. Use Copilot CLI to find the **root cause** (not just the symptom).
3. Apply the fix and verify "Dune Messiah" survives.

**Take 3 minutes**: Craft your own prompt to Copilot CLI. Think about what context Copilot needs (which file, which symptom, what you want back).

> 💡 **Hint**: Describe the symptom precisely — "When I do X, Y happens instead of Z." Reference the file with `@samples/book-app-buggy/books_buggy.py` and ask Copilot to explain the **root cause** before showing the fix.

<details>
<summary>✅ <b>Click to reveal the solution</b> (try it yourself first!)</summary>

**Example prompt:**

```bash
copilot

> @samples/book-app-buggy/books_buggy.py 
> When I remove "Dune", both "Dune" and "Dune Messiah" disappear. 
> Debug this: explain the root cause and provide a fix.
```

**What Copilot does:**
- Traces through the remove logic
- Finds a substring matching bug (using `in` instead of `==`)
- Shows you the exact line and the fix

**Expected output structure:**
```
Root Cause (Line 70):
The remove_book() function uses substring matching (the `in` operator) 
instead of exact matching.

Current code:
if title in book.title:  # BUG: "Dune" matches "Dune Messiah"!
    # remove book

Should be:
if title.lower() == book.title.lower():  # Exact match only
    # remove book
```

Another subtle bug caught! These are the kinds of bugs that ship to production. Testing would have caught these.

</details>

---

## Step 3: Understand the Debugging Workflow

Every time something breaks, follow this pattern:

1. **Describe the symptom**: "When I do X, Y happens instead of Z"
2. **Point Copilot to the code**: `@file-name`
3. **Ask why**: "Debug why this happens"
4. **Read the diagnosis**: Understand the root cause, not just the symptom
5. **Apply the fix**: Update the code
6. **Run tests**: Verify the fix works and doesn't break anything else

---

## ✨ Key Insight: Debugging

> Debugging isn't random guessing. It's **systematic thinking**:
> - Describe what you see (symptom)
> - Find where it happens (location)
> - Understand why (root cause)
> - Fix the root cause (not the symptom)

**Remember this**: If you find a bug, write a test for it. That bug becomes part of your test suite, so it never comes back.

---
# 🚀 MODULE 5: Parallel Analysis with /fleet Mode

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

## Key Insights: When to Use Fleet

### ✅ Use Fleet For:

- **Independent analyses**: Security, performance, and documentation are separate concerns
- **Multi-file reviews**: Analyze 5 different files or modules in parallel
- **Team scaling**: Each team member runs their own fleet simultaneously
- **Batch operations**: "Review all my recent PRs" across multiple branches

### ❌ Don't Use Fleet For:

- **Dependent tasks**: Don't run "refactor" and "test" in parallel if tests depend on refactoring
- **Sequential workflows**: The 4 main workflows (review → refactor → test → debug) have dependencies
- **Shared state**: If agents need to coordinate decisions, run them sequentially
- **Single-file analysis**: No benefit if you only have one thing to analyze
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

## Challenge: 4 Steps (20 minutes)

### Step 1: Understand the Scenario (2 minutes)

You're a project coordinator. Your job is to brief the orchestrator with one well-structured prompt and let it dispatch four parallel subagents.

**Context**:
- The **book-app** is your codebase
- You're deploying a new version Friday
- QA needs a baseline of issues
- There's a reported bug (mark-as-read behavior)
- Architecture needs improvement before production
- Test coverage is critical

Each work item targets a **discrete artifact** (a specific file or folder), so the orchestrator can parallelize them cleanly.

---

### Step 2: Start Copilot CLI (1 minute)

```bash
copilot
```

You're now at the interactive `>` prompt.

> 💡 **Pro workflow** (optional): Press **Shift+Tab** to enter plan mode, draft an implementation plan together with Copilot, then choose **"Accept plan and build on autopilot + /fleet"** to let Copilot execute the whole plan with subagents in parallel. For this exercise we'll use `/fleet` directly.

---

### Step 3: Launch All 4 Workstreams in One `/fleet` Prompt (5 minutes)

**Copy and paste this single prompt at the `>`:**

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

---

### Step 4: Monitor & Review Results (12 minutes)

**Check progress at the `>` prompt:**

```
/tasks
```

You'll see all 4 subtasks. Use ↑/↓ to navigate, Enter for details, `r` to remove finished tasks, Esc to exit. Wait until all report complete.

**When all agents finish**, review in this order:

**First**: Code Quality Audit findings
- What quality issues exist?
- Which are HIGH priority?
- Which align with what the Debug subagent found?

**Second**: Critical Bug findings
- What's the root cause?
- Does it match anything the Audit subagent flagged?
- How would the Refactor subagent's changes prevent it?

**Third**: Refactor findings
- What did it propose?
- Does it address the Audit's issues?
- Would it prevent bugs like the one the Debug subagent found?

**Fourth**: Test Generation findings
- Do the tests cover what the Audit and Debug subagents identified?
- Are edge cases covered?
- Would these tests catch the mark-as-read bug?

**Final Step**: Synthesis
- Notice how all four subagents contributed different perspectives on the *same codebase*
- The Audit found issues; Test Generation wrote tests for them
- Debug isolated a specific bug; Refactor's changes could prevent similar issues
- All happened simultaneously, from a single prompt

---

## Key Insights

### This Is How Professional Teams Operate

In real development:

- **QA teams** audit code quality continuously
- **Debugging specialists** fix reported bugs
- **Architecture leads** improve design
- **Test teams** ensure coverage

These happen **in parallel**, not sequentially. Each role doesn't wait for the others.

### Sequential vs. Parallel (The Speed Advantage)

**Sequential approach** (old way):
```
Agent 1 review:     10 minutes
Agent 2 debug:       8 minutes
Agent 3 refactor:   12 minutes
Agent 4 tests:      15 minutes
─────────────────────────────
TOTAL:              45 minutes
```

**Parallel approach** (with /fleet):
```
Agent 1 │ Agent 2 │ Agent 3 │ Agent 4
review  │  debug  │ refactor│  tests
 (10m)  │  (8m)   │  (12m)  │ (15m)
────────────────────────────────────
All run simultaneously = ~15 minutes
```

**Time saved: 30 minutes (67% faster)** on the same work.

### When to Use This Pattern

Use `/fleet` when:
- ✅ You have **independent work items** (different files, different concerns, different roles)
- ✅ Each item maps to a **discrete artifact** so the orchestrator can split cleanly
- ✅ Items don't block each other (review doesn't need test results first)
- ✅ You want **faster results** on complex codebases or multi-step plans

Skip `/fleet` when:
- ❌ Tasks are **sequentially dependent** (fix must be tested before shipping)
- ❌ Results from one task directly feed into the next (run them sequentially instead)
- ❌ The work is a single small change (overhead isn't worth it)

> ⚠️ **Heads up**: Each subagent runs its own LLM session, so `/fleet` typically consumes **more premium requests** than running the same work in a single session. Use it where the speedup is worth the cost. See [the official docs](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/fleet) for details.

### Mental Model: Vague Prompts Run Sequentially

The orchestrator only parallelizes work it can confidently split. If your prompt is vague or the dependencies are tangled, it may execute the work sequentially anyway. The fix is to **structure your prompt** with clearly numbered, independent items each pointing at a discrete artifact (file, folder, or concern) — exactly as we did in the basic and advanced challenges above.

### The Bigger Lesson

You've now seen /fleet used in two ways:

1. **Module 5 challenge**: Parallel *independent analyses* (security, performance, documentation)
2. **This stretch exercise**: Parallel *complete workflows* across *different task types* (review, debug, refactor, test)

The principle is the same: **identify independent work** and let Copilot CLI execute it in parallel.

This scales your productivity not just for analysis, but for complete development cycles.

</details>

---

---


# 💡 FOUR KEY LEARNINGS

## 1. Copilot CLI is Your Pair Programmer, Not a Magic Wand

It doesn't make decisions for you. You read its suggestions, you validate them, you decide. **You're in charge.**

Real impact: You stop wasting time on busywork (reading unfamiliar code, writing boilerplate tests, debugging by trial-and-error) and focus on the hard problems (architecture, edge cases, user experience).

## 2. Workflows Matter More Than Tools

The reason you shipped fast wasn't because Copilot CLI is magic. It was because you followed a **process**:

- Review (understand)
- Refactor (improve)
- Test (verify)
- Debug (fix)

**This process scales.** You'll use it tomorrow, next week, next year. The tool just makes it fast.

## 3. Speed Comes from Understanding, Not Shortcuts

Every developer inherits messy code. Every developer ships under pressure. That doesn't change. What changes is that **you now have a method.**

The reason you finished in an hour wasn't luck. It was method.

## 4. Parallelism Multiplies Your Method

Once you have a reliable method, the next leap is **doing more of it at once**. Fleet mode (`/fleet`) lets you run independent analyses and even complete workflows—review, refactor, test, debug—**in parallel** instead of one after another.

You saw this in Module 5: three analyses (security, performance, documentation) finished in the time it would normally take to do one. The principle generalizes: **identify independent work, then let Copilot CLI execute it concurrently.**

Sequential mastery makes you fast. Parallel execution makes you a force multiplier for your team.

---

# 📋 Quick Reference

Looking for the prompt templates from this workshop? They live in [QUICK-REFERENCE.md](./QUICK-REFERENCE.md) — save them for use on your own code.

---