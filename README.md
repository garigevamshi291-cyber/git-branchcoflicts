# 🚀 Git & GitHub — Complete Interview Preparation Guide
### By Garige Vamshi | Based on Personal Practice Repos

> **How to use this file:** Read it once before any interview. Every section has the concept, the command, what YOU practiced, and how to answer confidently.

---

## 📁 YOUR REPOSITORIES — Quick Reference

| Repo | What You Practiced |
|---|---|
| `test-garige` | First repo, README, basic commits |
| `git-demo--1` | init, add, commit, push, collaboration |
| `git` | Repo creation, empty repo understanding |
| `gitday-2-demo` | Python files in Git, multi-commit workflow |
| `Gitday-2-practice` | Infra/config files (RDS) in version control |
| `git-issue` | Flask app, GitHub Issues workflow |
| `flask-cicd-jenkins` | Jenkinsfile, Docker, CI/CD pipeline in Git |
| `ecommerce-eks-platform` | Terraform, K8s manifests, ArgoCD GitOps |

---

## 🧠 SECTION 1 — What is Git? (Always Asked First)

### Q: What is Git? What is the difference between Git and GitHub?

**Answer:**
Git is a **distributed version control system** that tracks changes in files over time. It lets multiple developers work on the same project simultaneously without overwriting each other's work.

GitHub is a **cloud-based hosting platform** for Git repositories. Git is the tool; GitHub is the service.

| Git | GitHub |
|---|---|
| Local tool installed on your machine | Cloud platform (website) |
| Tracks changes, manages versions | Hosts repos, enables collaboration |
| Works offline | Requires internet |
| Open source | Owned by Microsoft |

**Your example to say in interview:**
> "I used Git locally to manage all my project code — for example in my `ecommerce-eks-platform` project I used Git to version-control my Terraform files and Kubernetes manifests, and pushed everything to GitHub for visibility and collaboration."

---

## 🔧 SECTION 2 — Core Git Workflow (Day 1 Practice)

### The 4-Step Daily Git Workflow

```bash
git init               # Initialize a new repo (you did this in test-garige, git-demo--1)
git add .              # Stage all changes
git commit -m "msg"    # Save snapshot with message
git push origin main   # Push to GitHub
```

### Q: What is the difference between `git add` and `git commit`?

- `git add` — moves changes from **working directory → staging area** (you're saying "I want to include this")
- `git commit` — moves changes from **staging area → local repository** (you're saving the snapshot)
- `git push` — sends from **local repo → remote (GitHub)**

**Mental model:**
```
Working Directory  →  Staging Area  →  Local Repo  →  Remote (GitHub)
     (edit)          git add .        git commit       git push
```

### Q: What is `git status`? What is `git log`?

```bash
git status    # Shows what's staged, unstaged, untracked
git log       # Shows full commit history with hashes
git log --oneline  # Compact view — one line per commit
```

### Q: What does `git clone` do?

```bash
git clone https://github.com/garigevamshi291-cyber/git-issue.git
```
Creates a full local copy of a remote repository including all history.

---

## 🌿 SECTION 3 — Branching (Critical for Every Interview)

### Q: What is a branch? Why do we use branches?

A branch is an **independent line of development**. It lets you work on a feature or fix without affecting the main/stable code.

```bash
git branch                    # List all branches
git branch feature-login      # Create new branch
git checkout feature-login    # Switch to branch
git checkout -b feature-login # Create + switch in one command (shortcut)
git branch -d feature-login   # Delete branch after merge
```

### Q: What is the difference between `main` and `master`?

Both are just the **default branch name**. GitHub changed the default from `master` to `main` in 2020. They work identically — just a naming convention.

### Q: What is a HEAD in Git?

`HEAD` is a pointer that tells Git **which branch/commit you're currently on**. When you switch branches, HEAD moves. It always points to the latest commit of your current branch.

### Branching Strategy Used in Real DevOps Teams

```
main          ← production-ready code only
develop       ← integration branch
feature/xxx   ← individual feature work
hotfix/xxx    ← urgent production fixes
```

**Your example:**
> "In my `ecommerce-eks-platform` project I followed a branching strategy where I created feature branches for each microservice configuration and merged them into main only after testing."

---

## 🔀 SECTION 4 — Merging & Rebasing

### Q: What is `git merge`?

Combines changes from one branch into another. Creates a **merge commit**.

```bash
git checkout main
git merge feature-login    # Merges feature-login into main
```

### Q: What is a merge conflict? How do you resolve it?

A merge conflict happens when **two branches changed the same line** in a file differently. Git cannot auto-decide which version to keep.

```bash
# Git marks the conflict in the file like this:
<<<<<<< HEAD
return "linux dev"          ← your current branch version
=======
return "hello world"        ← incoming branch version
>>>>>>> feature-branch
```

**Resolution steps:**
1. Open the conflicted file
2. Manually choose which code to keep (or combine both)
3. Remove the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
4. `git add <file>`
5. `git commit`

### Q: What is the difference between `merge` and `rebase`?

| Merge | Rebase |
|---|---|
| Creates a merge commit | Re-applies commits on top of another branch |
| Preserves full history | Creates cleaner, linear history |
| Safer for shared branches | Use only on private/local branches |

```bash
git rebase main    # Reapply your branch commits on top of main
```

> **Interview tip:** Say "I prefer merge for shared branches like `main` and rebase for cleaning up my local feature branches before raising a PR."

---

## 🔄 SECTION 5 — Remote Operations

### Q: What is `origin`?

`origin` is the **default name** Git gives to the remote repository (GitHub URL). You can rename it but `origin` is the convention.

```bash
git remote -v                          # See remote URLs
git remote add origin <url>            # Add remote
git remote set-url origin <new-url>    # Change remote URL
```

### Q: Difference between `git fetch` and `git pull`?

| `git fetch` | `git pull` |
|---|---|
| Downloads changes from remote | Downloads + merges into current branch |
| Does NOT update your working files | Updates working files immediately |
| Safer — lets you review first | Quicker but auto-merges |

```bash
git fetch origin       # Download but don't merge
git pull origin main   # Download + merge = fetch + merge
```

### Q: What is `git push`?

```bash
git push origin main          # Push main branch to GitHub
git push origin feature-login # Push a specific branch
git push -u origin main       # Set upstream (first time only)
git push --force              # Force push (use carefully — overwrites remote)
```

---

## 📝 SECTION 6 — GitHub Issues (git-issue repo practice)

### Q: What is a GitHub Issue?

An Issue is a GitHub feature to **track bugs, features, tasks, or questions**. In your `git-issue` repo you practiced this workflow.

**Your Flask app in git-issue/app.py:**
```python
from flask import Flask
import os

app = Flask(__name__)

@app.route("/")
def hello():
    return "linux dev"

if __name__ == "__main__":
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

**Issue workflow you practiced:**
1. Open an Issue describing the bug/feature
2. Create a branch to fix it
3. Make changes → commit → push
4. Open Pull Request referencing the issue
5. Merge PR → Issue auto-closes with `Closes #1` in commit message

### Q: How do you link a commit to an Issue?

```bash
git commit -m "fix: resolve port binding bug Closes #1"
# GitHub automatically closes Issue #1 when this is merged to main
```

---

## 🔁 SECTION 7 — Pull Requests (You have "Pull Shark" badge!)

### Q: What is a Pull Request (PR)?

A PR is a **request to merge your branch into another branch**. It's the main way teams review code before it goes to production.

**PR Workflow:**
```
1. Create feature branch
2. Make changes + commit + push
3. Open PR on GitHub (feature → main)
4. Team reviews code, leaves comments
5. Address feedback, push new commits
6. PR approved → Merge
7. Delete feature branch
```

### Q: What is Code Review? Why is it important?

Code review is when **teammates read your PR** before it merges. It catches bugs, ensures code quality, shares knowledge across the team.

> You earned the **Pull Shark** achievement on GitHub — mention this! It means you successfully opened and merged Pull Requests.

---

## ↩️ SECTION 8 — Undoing Changes

### Q: How do you undo changes in Git?

This is one of the most common interview questions:

```bash
# 1. Undo unstaged changes (file not yet added)
git checkout -- filename.py
git restore filename.py          # newer syntax

# 2. Unstage a file (added but not committed)
git reset HEAD filename.py
git restore --staged filename.py # newer syntax

# 3. Undo last commit (keep changes in working dir)
git reset --soft HEAD~1

# 4. Undo last commit (remove changes completely) ⚠️ DANGEROUS
git reset --hard HEAD~1

# 5. Revert a commit (safe — creates new undo commit)
git revert <commit-hash>
```

### Q: Difference between `git reset` and `git revert`?

| `git reset` | `git revert` |
|---|---|
| Rewrites history | Adds a new "undo" commit |
| Dangerous on shared branches | Safe for shared/remote branches |
| Use on local private branches | Use on main/production branches |

---

## 🏷️ SECTION 9 — Tags & Releases

### Q: What are Git tags?

Tags mark **specific points in history** — usually version releases.

```bash
git tag                          # List all tags
git tag v1.0.0                   # Create lightweight tag
git tag -a v1.0.0 -m "Release"  # Annotated tag with message
git push origin v1.0.0           # Push tag to GitHub
git push origin --tags           # Push all tags
```

**Your context:** In the `ecommerce-eks-platform`, when you deployed a stable version of your Docker image, you'd tag it (`v1.0`, `v1.1`) so you can roll back if needed.

---

## 🙈 SECTION 10 — .gitignore

### Q: What is .gitignore?

A file that tells Git **which files/folders to never track**. Critical for security (don't commit secrets) and cleanliness.

```gitignore
# Python
__pycache__/
*.pyc
venv/

# Terraform
*.tfstate
*.tfstate.backup
.terraform/

# Secrets — NEVER commit these
*.env
.env
secrets.yaml
terraform.tfvars   # Contains AWS keys

# Docker
.dockerignore

# OS files
.DS_Store
Thumbs.db
```

**Your context:** In your `ecommerce-eks-platform` Terraform project, your `.gitignore` would exclude `terraform.tfstate` (contains sensitive infrastructure state) and `.env` files with AWS credentials.

---

## 🔁 SECTION 11 — GitOps & ArgoCD (Your Biggest Differentiator)

### Q: What is GitOps?

GitOps is a practice where **Git is the single source of truth** for infrastructure and application deployments. You practiced this in `ecommerce-eks-platform` with ArgoCD.

**How it works:**
```
Developer pushes code to Git
        ↓
GitHub Actions builds Docker image, updates manifest
        ↓
ArgoCD detects change in Git repo
        ↓
ArgoCD automatically syncs Kubernetes cluster to match Git state
```

### Q: What is ArgoCD?

ArgoCD is a **GitOps continuous delivery tool for Kubernetes**. It watches your Git repo and automatically applies changes to your cluster.

**Your hands-on experience:**
> "In my EKS project I configured ArgoCD to watch my GitHub repository. Whenever I pushed updated Kubernetes manifests, ArgoCD would automatically sync the changes to the EKS cluster — no manual `kubectl apply` needed. This is true GitOps."

---

## ⚙️ SECTION 12 — GitHub Actions (CI/CD in Git)

### Q: What is GitHub Actions?

GitHub Actions is GitHub's built-in **CI/CD automation platform**. You practiced this in `flask-cicd-jenkins` and `ecommerce-eks-platform`.

**Typical workflow file** (`.github/workflows/deploy.yml`):
```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [main]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Build Docker image
        run: docker build -t myapp:${{ github.sha }} .

      - name: Push to ECR
        run: |
          aws ecr get-login-password | docker login --username AWS ...
          docker push myapp:${{ github.sha }}

      - name: Deploy to EKS
        run: kubectl apply -f k8s/
```

**Your answer:**
> "I built GitHub Actions pipelines in my e-commerce project that automatically built Docker images on every push to main, pushed them to AWS ECR, and updated the Kubernetes deployment — cutting deployment time from 30 minutes to under 10 minutes."

---

## 📊 SECTION 13 — Git Commands Cheat Sheet

### Essential Commands (Know These Cold)

```bash
# SETUP
git config --global user.name "Vamshi"
git config --global user.email "garigevamshi291@gmail.com"

# START
git init                          # New repo
git clone <url>                   # Copy existing repo

# DAILY WORKFLOW
git status                        # What's changed?
git add .                         # Stage everything
git add filename.py               # Stage specific file
git commit -m "feat: add login"   # Commit with message
git push origin main              # Push to GitHub
git pull origin main              # Get latest from GitHub

# BRANCHING
git branch                        # List branches
git checkout -b feature-name      # Create + switch
git merge feature-name            # Merge into current
git branch -d feature-name        # Delete branch

# INSPECT
git log --oneline                 # Compact history
git diff                          # See unstaged changes
git show <commit-hash>            # See specific commit

# UNDO
git restore filename.py           # Discard local changes
git restore --staged filename.py  # Unstage file
git reset --soft HEAD~1           # Undo last commit (keep changes)
git revert <hash>                 # Safe undo (adds new commit)

# STASH (pause work temporarily)
git stash                         # Save current work temporarily
git stash pop                     # Restore stashed work
git stash list                    # List all stashes

# REMOTE
git remote -v                     # See remotes
git fetch origin                  # Download without merging
git pull origin main              # Download + merge
```

---

## 💬 SECTION 14 — Top 20 Interview Questions & Answers

**Q1: What is version control and why is it important?**
Version control tracks every change made to code over time. It lets teams collaborate, revert mistakes, and maintain history. Without it, coordinating code changes across teams would be chaos.

**Q2: What is a commit? What makes a good commit message?**
A commit is a saved snapshot of your changes. A good commit message is short, descriptive, and uses a prefix: `feat:`, `fix:`, `chore:`, `docs:`. Example: `feat: add health check endpoint to Flask app`.

**Q3: What is the difference between `git pull` and `git fetch`?**
`git fetch` downloads remote changes but doesn't apply them. `git pull` = fetch + merge. Use fetch when you want to review changes before merging.

**Q4: How do you handle a merge conflict?**
Edit the conflicting file to keep the correct code, remove Git's conflict markers, then `git add` and `git commit`. In teams, always communicate before editing shared files.

**Q5: What is a fork? How is it different from a clone?**
A fork creates a **copy of someone else's repo in your GitHub account**. A clone creates a local copy on your machine. You fork to contribute to open source projects.

**Q6: What is `git stash`?**
Stash temporarily saves your uncommitted changes so you can switch branches without losing work. `git stash pop` restores them.

**Q7: What is cherry-pick?**
`git cherry-pick <hash>` applies a **single specific commit** from one branch to another — without merging the whole branch.

**Q8: What is `git blame`?**
`git blame filename` shows **who last changed each line** of a file and in which commit. Used for debugging — to find who introduced a bug.

**Q9: What is a detached HEAD state?**
When you checkout a specific commit (not a branch), HEAD points directly to that commit instead of a branch. Any commits made won't belong to any branch.

**Q10: What is `git bisect`?**
A binary search tool to find **which commit introduced a bug**. You mark a good commit and a bad commit, and Git helps you narrow down the culprit.

**Q11: Explain your Git workflow in your EKS project.**
> "I used a trunk-based workflow. Feature branches for each component (networking, compute, monitoring). GitHub Actions triggered on push to main — it built Docker images, pushed to ECR, and ArgoCD synced to EKS automatically. Every infrastructure change went through Git, making rollback easy."

**Q12: How do you roll back a bad deployment using Git?**
```bash
git revert <bad-commit-hash>   # Creates undo commit
git push origin main            # Triggers CI/CD to redeploy old config
```
With ArgoCD, reverting the Git commit automatically reverts the Kubernetes state.

**Q13: What is a `.git` folder?**
Hidden folder in every Git repo containing all the metadata — commit history, branches, config, HEAD pointer. Never delete or edit it manually.

**Q14: What is the difference between `git reset --soft`, `--mixed`, and `--hard`?**
- `--soft`: Undo commit, keep changes staged
- `--mixed` (default): Undo commit, keep changes unstaged
- `--hard`: Undo commit, delete all changes permanently

**Q15: What is squashing commits?**
Combining multiple commits into one before merging a PR, for a cleaner history.
```bash
git rebase -i HEAD~3   # Squash last 3 commits
```

**Q16: How do you clone a specific branch?**
```bash
git clone -b feature-branch <url>
```

**Q17: What is `git remote prune origin`?**
Removes references to remote branches that have been deleted on GitHub but still appear locally.

**Q18: Can you explain the GitHub Pull Shark achievement you have?**
> "Yes, that badge means I successfully opened and merged multiple Pull Requests on GitHub. It confirms I've practiced the real collaborative workflow — branching, pushing, opening PRs, and merging — not just local Git usage."

**Q19: How do you protect the `main` branch?**
In GitHub repository Settings → Branches → Branch protection rules: require PR reviews before merge, require status checks to pass (CI), prevent force pushes.

**Q20: What is the difference between `git diff` and `git diff --staged`?**
- `git diff` — shows changes not yet staged
- `git diff --staged` — shows changes staged but not yet committed

---

## 🎯 SECTION 15 — How to Talk About YOUR Git Experience

### Story 1: Day 1 Learning
> "I started with the basics — creating my first repository `test-garige` on GitHub, initializing Git locally, staging files, making commits, and pushing. It sounds simple but understanding the working directory → staging area → local repo → remote flow is foundational."

### Story 2: Python + Issues Workflow
> "In my `git-issue` repo I built a simple Flask application and practiced the GitHub Issues workflow — tracking bugs as Issues, creating fix branches, and closing Issues via commit messages. This mirrors how real DevOps teams manage work."

### Story 3: Infrastructure as Code in Git
> "In `Gitday-2-practice` I specifically practiced version-controlling infrastructure config files, not just application code. An `rds` config file in Git means your database configuration is trackable, auditable, and rollback-able — that's the DevOps mindset."

### Story 4: Full GitOps Pipeline
> "My most advanced Git work was the `ecommerce-eks-platform`. Every piece of infrastructure — VPC, EKS cluster, RDS, IAM — was written as Terraform code and committed to Git. GitHub Actions built and pushed Docker images on each commit. ArgoCD watched the repo and synced Kubernetes automatically. The Git repo was literally the control plane for the entire production environment."

---

## ⚡ SECTION 16 — Quick Revision (5 Minutes Before Interview)

**Git = distributed version control. GitHub = hosting platform.**

**3 states:** Working Directory → Staging Area → Repository

**4 daily commands:** `git add` → `git commit` → `git push` → `git pull`

**Branching:** Always work on feature branches, merge to main via PR

**Conflict:** Edit file → remove markers → add → commit

**Undo safely:** `git revert` (adds new commit, safe for shared branches)

**GitOps:** Git is the source of truth → ArgoCD syncs cluster to Git state

**Your badge:** Pull Shark = you merged real Pull Requests

**Your projects:**
- `git-issue` → Flask app + GitHub Issues workflow
- `flask-cicd-jenkins` → Jenkins + Docker CI/CD pipeline
- `ecommerce-eks-platform` → Full GitOps: Terraform + K8s + ArgoCD + GitHub Actions

---

*Prepared by Garige Vamshi | github.com/garigevamshi291-cyber*
*Keep this file handy — open it 5 minutes before every interview.*
