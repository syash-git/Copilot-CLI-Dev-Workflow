# 🐛 MODULE 4: DEBUGGING (13 minutes)

> 🧭 Module 4 of 5 · [Workshop index](../README.md) · Previous: [Module 3 — Test Generation](./03-test-generation.md) · Next: [Module 5 — Parallel Analysis with /fleet](./05-fleet-mode.md)

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

### 👉 Next up: Module 5 — Parallel Analysis with /fleet

You can now run the full review → refactor → test → debug loop on one module. The final module shows how to run several of these workflows in parallel with /fleet.

[**Continue → Module 5 — Parallel Analysis with /fleet**](./05-fleet-mode.md)
