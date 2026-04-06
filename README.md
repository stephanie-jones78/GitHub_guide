# git push origin main
## A Complete GitHub Starter Guide — From Zero to Publishing

An interactive guide for developers who are ready to work like professionals. Takes you from never having touched a terminal to having a live project on GitHub with a public URL you can share with anyone.

---

## Live Demo

**[Open the guide →]([https://github.com/stephanie-jones78.github.io/index)](https://stephanie-jones78.github.io/GitHub_guide/)**

*(Update this link with your username after you deploy)*

---

## What This Is

Most GitHub tutorials throw commands at you without explaining what they're doing or why. This guide is different. It starts with the mental model — what Git and GitHub actually are and how they relate — then builds to real commands, real workflows, and a real deployed project.

By the time you finish, you will have:
- A configured local Git environment
- SSH authentication set up correctly (no more password confusion)
- A GitHub profile with at least one public repo
- A live website deployed free via GitHub Pages
- The daily workflow committed to muscle memory

---

## What's Covered

| Section | What You'll Do |
|---|---|
| **The Mental Model** | Understand what Git and GitHub actually are before touching a command |
| **Core Concepts** | Repo, commit, branch, staging, push/pull, merge — the six ideas everything else builds on |
| **Setup** | Install Git, configure your identity, generate SSH keys, connect to GitHub |
| **The Daily Workflow** | The 7 commands you use every single day |
| **Branches** | Build features safely without breaking what works |
| **Publish Live** | Deploy your project as a live website via GitHub Pages — free, in under 5 minutes |
| **Build in Public** | Habits that make your profile a real portfolio |

---

## How to Use This Guide

### Option A — Online (recommended, full interactivity)
Open the live URL above. Everything works — tap cards, quizzes, copy buttons, checklist.

### Option B — Locally on Mac or Windows
Download `index.html`. Double-click to open in your browser.
> Note: Interactive elements require the file to be served from a URL. Layout and content are fully readable locally, but for full interactivity use Option A or host your own copy.

### Option C — Host your own copy
Fork this repo, enable GitHub Pages, and share your own URL. The guide walks you through exactly this.

---

## Complete Setup Walkthrough

### 1. Create your GitHub account
Go to `github.com/signup`. Choose a professional username — it becomes part of your public URL (`github.com/yourname`) and is hard to change later without breaking existing links.

### 2. Install Git
**Mac:** Open Terminal, run `git --version`. If not installed, macOS will prompt you automatically via Xcode Command Line Tools.
**Windows:** Download from `git-scm.com`, run installer with all defaults.

### 3. Configure your identity
```bash
git config --global user.name "Your Name"
git config --global user.email "you@email.com"
git config --global init.defaultBranch main
```

### 4. Set up SSH authentication

**Why SSH?** GitHub removed password authentication from the terminal in 2021. Your account password only works on the website. The terminal uses SSH keys — your machine proves its identity cryptographically instead of with a password. Set this up once and you never authenticate manually again.

**How it works:** SSH creates two mathematically linked keys. The private key stays on your machine only. The public key goes to GitHub. When you push code, your machine and GitHub do a silent handshake. No password. No prompt. Just works.

**Generate your key pair:**
```bash
ssh-keygen -t ed25519 -C "you@email.com"
# Press Enter 3 times to accept all defaults
```

This creates two files in `~/.ssh/`:
- `id_ed25519` — your **private key**. Never share this. Never copy it anywhere.
- `id_ed25519.pub` — your **public key**. This is what goes to GitHub.

**Common confusion point:** After generating, Terminal prints a fingerprint starting with `SHA256:` and some random art. That is **not** your key — it's just a visual confirmation the key was created. Your actual key is in the `.pub` file.

**Copy your public key to clipboard:**
```bash
cat ~/.ssh/id_ed25519.pub | pbcopy
```
*(Mac only — copies silently. Windows: run `cat ~/.ssh/id_ed25519.pub` and manually select and copy the output.)*

What you're copying is one long line starting with `ssh-ed25519` and ending with your email. If it starts with `SHA256` — that's the fingerprint, not the key. Re-run the `cat` command above.

**Add it to GitHub:**
Profile photo → **Settings** → **SSH and GPG keys** → **New SSH key** → paste → **Add SSH key**

**Verify the connection:**
```bash
ssh -T git@github.com
# Should say: Hi username! You've successfully authenticated.
```

### 5. Create your first repo

On GitHub: **+** → **New repository** → name it → Public → **do not** check any initialization boxes → **Create**

Then in Terminal:
```bash
mkdir my-project
cd my-project
git init
git add .
git commit -m "initial commit"
git remote add origin git@github.com:YOURUSERNAME/my-project.git
git branch -M main
git push -u origin main
```

### 6. The daily workflow
```bash
git status                            # what changed since last commit
git add .                             # stage everything
git commit -m "what changed and why"  # save the snapshot
git push                              # send to GitHub
git pull                              # get latest (when collaborating)
```

### 7. Deploy a live website (GitHub Pages)

Your repo needs an `index.html` at the root. Then on GitHub:

**Settings** → **Pages** → Source: **Deploy from a branch** → Branch: **main** → **Save**

Wait ~60 seconds. Live at:
```
https://YOURUSERNAME.github.io/REPO-NAME
```

---

## Troubleshooting

**`error: failed to push some refs`**
GitHub has commits your local machine doesn't. Run `git pull origin main --rebase` then push again.

**`fatal: Updating an unborn branch`**
You haven't made your first commit yet. Run `git add .` and `git commit -m "initial commit"` before pushing.

**`remote origin already exists`**
Skip the `git remote add` line. Run `git branch -M main && git push -u origin main` directly.

**Password rejected in terminal**
Expected behavior — GitHub doesn't accept passwords in the terminal. Use SSH (Section 4 above). If you need a faster workaround, generate a Personal Access Token: GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic) → Generate new token → check `repo` scope → paste the token wherever a password is requested.

**"Key is invalid" when adding SSH key to GitHub**
You likely copied the fingerprint (`SHA256:...`) instead of the actual public key. Run `cat ~/.ssh/id_ed25519.pub` — copy the output that starts with `ssh-ed25519`, not `SHA256`.

**`remote: Repository not found`**
Your remote URL may be using HTTPS instead of SSH. Check with `git remote -v` and update if needed:
```bash
git remote set-url origin git@github.com:YOURUSERNAME/REPO-NAME.git
```

---

## Stack

- Vanilla HTML, CSS, JavaScript
- Zero dependencies
- No build step
- Fully interactive when served from a URL

---

## About

Built as a teaching resource for developers starting from zero. Fork it, adapt it, share it.
