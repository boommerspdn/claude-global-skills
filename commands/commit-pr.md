---
description: Stage changes, create a conventional commit, push to remote, and open a GitHub PR with a structured description. Use when the user wants to commit their work and open a pull request.
argument-hint: [optional commit hint]
allowed-tools: Bash, Read
---

You are helping the user commit their changes and open a pull request. Follow these steps carefully.

## Step 1: Safety Checks

Run `git branch --show-current` and abort with a clear message if the branch is `main` or `master`. Tell the user to create a feature branch first.

## Step 2: Inspect Changes

Run these in parallel:
- `git status` — see what files changed
- `git diff HEAD` — understand the nature of changes
- `git log --oneline -5` — learn this repo's commit message style

## Step 3: Stage Files

Stage all modified tracked files. Skip any of these if they appear:
- `.env` or `.env.*`
- `application-local.yaml` or `application-local.yml`
- `firebase-service-account.json`
- Any file ending in `.key`, `.pem`, `.p12`

Show the user exactly what was staged.

## Step 4: Write the Commit Message

Infer the conventional commit type from the diff:
- `feat` — new feature or endpoint
- `fix` — bug fix
- `chore` — dependencies, config, build, docker
- `docs` — documentation only
- `refactor` — restructuring without behavior change
- `test` — tests only
- `ci` — CI/CD pipeline changes
- `security` — vulnerability fixes, dependency upgrades for CVEs

Infer the scope from the files changed (e.g., `auth`, `payment`, `docker`, `deps`).

Format: `type(scope): short imperative description`

If the user provided `$ARGUMENTS`, use it as a hint for the description.

Commit using a HEREDOC:
```bash
git commit -m "$(cat <<'EOF'
type(scope): description
EOF
)"
```

## Step 5: Push

```bash
git push -u origin HEAD
```

## Step 6: Create the Pull Request

Use `gh pr create` with this body structure (pass via HEREDOC):

```
## Summary
- concise bullet points of what changed and why

## Type of change
- [ ] Bug fix
- [ ] New feature
- [ ] Refactor
- [ ] Dependency / security update
- [ ] Config / infra

## Test plan
- [ ] Describe how to verify this works

🤖 Generated with [Claude Code](https://claude.com/claude-code)
```

Set `--base main` and `--title` to the commit subject line.

Return the PR URL to the user when done.
