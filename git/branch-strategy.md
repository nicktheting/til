# Git — Branch Strategy

## The Three-Branch Model

```
main    → production (what runs on the live server)
stage   → staging (testing before production)
dev     → development (daily work)
```

---

## Setup

```bash
# Create and push all branches
git checkout -b dev
git push -u origin dev

git checkout -b stage
git push -u origin stage
```

---

## Daily Workflow

```bash
# Always work on dev
git checkout dev

# Make changes and commit
git add .
git commit -m "description of change"
git push

# Merge into stage for testing
git checkout stage
git merge dev
git push

# Deploy to production via Pull Request on GitHub
# stage → main
```

---

## Branch Protection (main)

On GitHub: **Settings → Branches → Add branch ruleset**

- ✅ Restrict deletions
- ✅ Require a pull request before merging
- ✅ Block force pushes

This ensures nothing goes to `main` without a Pull Request.

---

## Commit Message Convention

```
feat: add new feature
fix: bug fix
style: CSS/styling changes
refactor: code refactor
docs: documentation update
chore: config/setup changes
```

**Examples:**
```bash
git commit -m "feat: add child theme"
git commit -m "fix: disable storage warning in dev"
git commit -m "style: update header styles"
git commit -m "docs: add child theme guide"
```

---

## Golden Rules

- ✅ Always work on `dev`
- ✅ Test on `stage` before going to `main`
- ✅ Use descriptive commit messages
- ❌ Never push directly to `main`
- ❌ Never merge untested code to `main`
