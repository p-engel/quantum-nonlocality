# GitHub Repo Setup Guide
## Step-by-step: Create, push, and invite a collaborator

---

### Step 1 — Create the repo on GitHub

1. Go to [github.com/new](https://github.com/new)
2. Set:
   - **Repository name:** `quantum-info-repo` (or your preferred name)
   - **Visibility:** Public or Private (Private recommended until you're ready to share)
   - **Do NOT** initialize with README (you'll push your own)
3. Click **Create repository**

---

### Step 2 — Push these files from your local machine

```bash
# In your terminal, navigate to this folder
cd quantum-info-repo

# Initialize git
git init
git add .
git commit -m "Initial commit: repo scaffold, README, Qiskit starter notebooks"

# Link to your GitHub repo (replace with your actual URL)
git remote add origin https://github.com/p-engel/quantum-info-repo.git

# Push
git branch -M main
git push -u origin main
```

---

### Step 3 — Invite your collaborator

1. On the repo page, go to **Settings → Collaborators → Add people**
2. Search by your colleague's GitHub username or email
3. Click **Add collaborator**
4. They'll receive an email — once they accept, they have push access

**Your collaborator then runs:**
```bash
git clone https://github.com/p-engel/quantum-info-repo.git
```

---

### Step 4 — Recommended branch protection (optional but good practice)

In **Settings → Branches → Add branch protection rule:**
- Branch name pattern: `main`
- ✅ Require pull request reviews before merging
- ✅ Require status checks to pass (if you add CI later)

This means neither of you can push directly to `main` — you both work on branches and merge via PRs.

---

### Daily workflow

```bash
# Start new work
git checkout dev
git pull origin dev
git checkout -b feature/your-feature-name

# ... work, save files ...

git add .
git commit -m "Description of what you did"
git push origin feature/your-feature-name

# On GitHub: open a Pull Request from feature/... → dev
# Colleague reviews → merge → done
```

---

### Keeping notebooks clean for version control

Jupyter notebooks store cell outputs (plots, print statements) in the `.ipynb` JSON, which makes diffs messy. Options:

**Option A (simple):** Clear outputs before committing
```bash
jupyter nbconvert --clear-output --inplace notebooks/*.ipynb
```

**Option B (automated):** Add `nbstripout` to your git hooks
```bash
pip install nbstripout
nbstripout --install   # strips outputs automatically on every commit
```

---

### .gitignore (add this to your repo root)

```
__pycache__/
*.py[cod]
.ipynb_checkpoints/
.env
*.egg-info/
dist/
build/
.DS_Store
*.log
```
