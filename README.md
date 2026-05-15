# claude-global-skills

Global Claude Code slash commands, available across all projects.

---

## Setup

### 1. Clone the repo

```bash
git clone https://github.com/boommerspdn/claude-global-skills ~/Documents/GitHub/claude-global-skills
```

### 2. Symlink commands into Claude Code

```bash
ln -s ~/Documents/GitHub/claude-global-skills/commands ~/.claude/commands
```

> Claude Code automatically picks up any `.md` files in `~/.claude/commands/` as slash commands.

### 3. Verify

Open Claude Code and type `/` — your commands should appear in autocomplete.

---

## Directory Structure

```
claude-global-skills/
├── README.md
└── commands/               # Each .md file becomes a /command-name
    └── commit-pr.md        # /commit-pr — commit changes and open a PR
```

---

## Adding a New Command

1. Create `commands/your-command-name.md` with this frontmatter:

```markdown
---
description: What this command does (shown in /help)
argument-hint: [optional args]
allowed-tools: Bash, Read
---

Your command instructions here...
```

2. Commit and push — the symlink means it's live immediately, no restart needed.

---

## Commands

| Command | Description |
|---|---|
| `/commit-pr` | Stage changes, create a conventional commit, push, and open a GitHub PR |
