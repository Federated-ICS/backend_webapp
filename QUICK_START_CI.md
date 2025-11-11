# Quick Start: GitHub Actions CI/CD

## 🚀 5-Minute Setup

### 1. Push to GitHub (1 min)

```bash
git add .
git commit -m "Add CI/CD pipeline"
git push origin main
```

### 2. Enable Actions (30 sec)

1. Go to your repo on GitHub
2. Click **"Actions"** tab
3. Click **"I understand my workflows, go ahead and enable them"** (if prompted)

### 3. Watch It Run! (5-7 min)

You'll see three workflows start automatically:
- 🔵 CI Pipeline (running)
- 🔵 Quick Check (running)
- 🔵 Security Scan (running)

Wait for them to turn green ✅

### 4. Update Badges (1 min)

In `README.md`, replace:
- `YOUR_USERNAME` → your GitHub username
- `YOUR_REPO` → your repository name

Example:
```markdown
[![CI Pipeline](https://github.com/johndoe/ics-backend/actions/workflows/ci.yml/badge.svg)]
```

### 5. Done! 🎉

Your CI/CD pipeline is now active!

---

## 📋 Quick Checklist

- [ ] Code pushed to GitHub
- [ ] Actions tab shows workflows
- [ ] All workflows pass (green ✅)
- [ ] Badges updated in README
- [ ] Badges show "passing"

---

## 🔧 If Something Fails

### Tests Fail?
```bash
make test
# Fix issues, then:
git add .
git commit -m "Fix tests"
git push
```

### Linting Fails?
```bash
make format
git add .
git commit -m "Fix formatting"
git push
```

### Still Having Issues?
```bash
# Run all checks locally
make ci

# This runs the same checks as GitHub Actions
```

---

## 🎯 What's Running?

Every time you push, GitHub automatically:

1. **Runs all tests** with PostgreSQL
2. **Checks code quality** (formatting, linting)
3. **Performs type checking** with mypy
4. **Scans for security issues**
5. **Reports coverage** to Codecov (optional)

All in parallel, taking ~5-7 minutes total.

---

## 📊 View Results

### In GitHub:
- **Actions tab** → See all workflow runs
- **Pull Requests** → See checks on each PR
- **README** → Status badges

### Locally:
```bash
make ci  # Run same checks locally
```

---

## 🛡️ Optional: Branch Protection

Require CI to pass before merging:

1. Settings → Branches
2. Add rule for `main`
3. Enable "Require status checks to pass"
4. Select: `test`, `lint`, `type-check`, `quick-test`
5. Save

Now PRs can't merge until CI passes! ✅

---

## 💡 Pro Tips

1. **Run `make ci` before pushing** to catch issues early
2. **Install pre-commit hooks** with `make pre-commit`
3. **Check Actions tab** if builds fail
4. **Use `make format`** to auto-fix formatting issues

---

## 📚 More Info

- [GITHUB_SETUP_GUIDE.md](GITHUB_SETUP_GUIDE.md) - Detailed setup
- [docs/CI_CD.md](docs/CI_CD.md) - Complete documentation
- [docs/CI_SETUP.md](docs/CI_SETUP.md) - Step-by-step guide

---

**That's it!** Your CI/CD pipeline is ready. Happy coding! 🚀
