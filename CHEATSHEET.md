# 🧰 Copilot CLI Cheatsheet

A scannable reference for the **Copilot CLI itself** — slash commands, keyboard shortcuts, mention prefixes, and modes.

> Looking for **prompt templates** (review / refactor / test / debug)? See [`QUICK-REFERENCE.md`](./QUICK-REFERENCE.md).
> New here? Start with the [workshop](./README.md).

---

## 🚀 Launch & Exit

| Command | What it does |
|---|---|
| `copilot` | Start an interactive Copilot CLI session. |
| `copilot --banner` | Start with the ASCII banner. |
| `copilot --experimental` | Enable experimental features. |
| `/exit` *or* `Ctrl+D` | End the session. |
| `Ctrl+C` (×2) | Cancel current action; press twice to quit. |

---

## ✍️ Mention Syntax (inside a prompt)

| Prefix | Meaning | Example |
|---|---|---|
| `@` | Reference a file or folder | `Review @samples/book-app-project/book_app.py` |
| `#` | Reference an issue or PR | `Summarize #42` |
| `!` | Run a shell command inline | `!git status` |
| `/` | Slash command (see below) | `/plan add input validation` |

---

## 🔀 Modes — cycle with `Shift+Tab`

| Mode | When to use |
|---|---|
| **Normal** | Default. Copilot edits as it goes. |
| **Plan** | Copilot drafts a plan first, waits for approval before changing code. Great for multi-step work. |
| **Autopilot** | Copilot runs through the task without prompting for approvals. Use for trusted, well-scoped tasks. |

You can also enter Plan Mode for a single prompt with `/plan <goal>`.

---

## ⚡ Most-Used Slash Commands

### Planning & parallel execution
| Command | Purpose |
|---|---|
| `/plan <goal>` | Draft a plan before any code changes. |
| `/fleet <task>` | Run multiple sub-agents in parallel on independent subtasks. |
| `/tasks` | View / manage the current task list. |

### Code
| Command | Purpose |
|---|---|
| `/review` | Review staged or recent changes. |
| `/diff` | Show the current diff. |
| `/pr` | Create or update a pull request from the session. |

### Sessions
| Command | Purpose |
|---|---|
| `/new` | Start a fresh session. |
| `/resume` | Resume a previous session. |
| `/compact` | Summarize history to free up context. |
| `/clear` | Clear the current screen. |
| `/rewind` | Step back to an earlier turn. |
| `/undo` | Revert the last edit. |
| `/share` | Share a session link. |

### Models, context & quota
| Command | Purpose |
|---|---|
| `/model` | Switch the active model. |
| `/context` | Inspect what's currently in context. |
| `/usage` | Show token usage for the session. |

### Permissions & environment
| Command | Purpose |
|---|---|
| `/add-dir` | Grant access to an additional directory. |
| `/allow-all` | Auto-approve tool calls for the session. |
| `/cwd` | Show or change the working directory. |
| `/mcp` | Manage MCP server connections. |

### Help & utility
| Command | Purpose |
|---|---|
| `/help` | List every slash command. |
| `/init` | Generate a starter `AGENTS.md` for the repo. |
| `/login` · `/logout` | Manage GitHub authentication. |
| `/feedback` | Send feedback to the Copilot team. |
| `/version` · `/update` | Check version / update the CLI. |

---

## ⌨️ Keyboard Shortcuts

### Global
| Keys | Action |
|---|---|
| `Shift+Tab` | Cycle modes (normal → plan → autopilot). |
| `Ctrl+C` | Cancel current action. |
| `Ctrl+C` ×2 | Exit the session. |
| `Ctrl+D` | Shut down the CLI. |
| `Ctrl+L` | Clear the screen. |
| `Ctrl+T` | Toggle reasoning display. |
| `Ctrl+X` → `B` | Send the running task to the background. |
| `Esc` | Cancel the current prompt. |

### Input editing
| Keys | Action |
|---|---|
| `Ctrl+G` | Open the current prompt in `$EDITOR`. |
| `Ctrl+A` / `Ctrl+E` | Jump to start / end of line. |
| `Ctrl+W` | Delete previous word. |
| `Ctrl+U` / `Ctrl+K` | Delete to start / end of line. |
| `Ctrl+H` | Backspace. |

---

## 📄 Instruction Files Copilot Reads

Drop project-specific guidance in any of these and Copilot will pick it up:

- `AGENTS.md` — primary instruction file for this repo (create with `/init`).
- `.github/copilot-instructions.md` — repo-wide rules.
- `CLAUDE.md` — also recognized.

---

## 🔗 See Also

- [`QUICK-REFERENCE.md`](./QUICK-REFERENCE.md) — prompt templates for review, refactor, tests, debugging.
- [`README.md`](./README.md) — the workshop, with all of the above used in context.
- [`TROUBLESHOOTING.md`](./TROUBLESHOOTING.md) — setup issues and fixes.
