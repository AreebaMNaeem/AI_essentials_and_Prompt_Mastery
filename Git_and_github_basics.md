# 🌿 Git and GitHub Basics: A Student Guide

> Learn how to save your project's history, back it up online, and keep your work organized, step by step.

---

## 💡 What is Git?

Git is a **version control system** and a **tracking system** for your files.

- **Version control:** keeps every version of your project, so you can go back if something breaks
- **Tracking system:** records what changed, when, and who changed it
- **One folder:** no more `project_final`, `project_final2`, `project_FINAL_really`
- **How it saves your work:** every time you save in Git, it takes a snapshot called a **commit**
- **Where it all lives:** your project folder plus all its commits is called a **repository** (or **repo**)
- Runs on your computer, works offline, and is free

---

## 🌐 What is GitHub?

GitHub is a website that stores your Git projects **online**.

- Backs up your project
- Makes it easy to share
- Available from any device

**Git is the tool. GitHub is the website.**

---

## ⚙️ Setup

**1. Install Git** from [git-scm.com](https://git-scm.com) and check it worked:
```bash
git --version
```

**2. Tell Git who you are** (only once per computer):
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```
Use the same email as your GitHub account.

**3. Create a free account** at [github.com](https://github.com).

---

## 🔄 The Git Workflow

`git init` starts the tracking. After that, your files move through four places:

```
        git init
   (start tracking the folder)
              │
              ▼
   Working Directory     (your files)
              │  git add
              ▼
   Staging Area          (ready to save)
              │  git commit  →  a commit ID is created here
              ▼
   Local Repository      (saved history)
              │  git push
              ▼
   GitHub                (online copy)
```

| Place | What it means |
|---|---|
| **Working Directory** | The folder where you edit your files |
| **Staging Area** | A waiting area where you choose what goes into the next save |
| **Local Repository** | Your saved history (commits) on your computer |
| **Remote (GitHub)** | The online copy of your repository |

**Real-life example:** think of packing a parcel. Your items on the table are the working directory, the items you put in the box are the staging area, sealing the box is the commit, and sending it is the push.

---

## 🚀 Your First Repository, Step by Step

### Step 1: Initialize (`git init`)

Create a folder, open a terminal inside it, and run:
```bash
mkdir my-first-repo
cd my-first-repo
git init
```
This creates a hidden `.git` folder where Git stores your history. Your folder is now a repository.

### Step 2: Create a file and check the status (`git status`)

```bash
echo "# My First Repo" > README.md
git status
```
Git shows `README.md` as **untracked**. It sees the file but isn't tracking it yet.

> Run `git status` often. It always tells you what is going on.

### Step 3: Stage your changes (`git add`)

```bash
git add README.md
```
To stage everything at once:
```bash
git add .
```
Run `git status` again. The file is now **staged** (ready to be committed).

### Step 4: Commit (`git commit`)

```bash
git commit -m "Add README file"
```
A **commit** is a saved snapshot of your staged changes, with a message describing what you did.

Git also creates a unique **commit ID** at this moment. You will see it in the output:
```
[main (root-commit) a1b2c3d] Add README file
```
Here `a1b2c3d` is the commit ID (yours will look different). You can see all your commit IDs later with `git log --oneline`.

**Good commit messages are short and clear:**
- ✅ `Add login page`
- ✅ `Fix typo in README`
- ❌ `stuff`
- ❌ `final final 2`

### Step 5: Create a repository on GitHub

1. Log in to GitHub and click **New repository**.
2. Give it a name (for example `my-first-repo`).
3. Leave it empty (don't add a README there, since you already have one).
4. Click **Create repository** and copy the repository URL.

### Step 6: Connect and push (`git remote`, `git push`)

```bash
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/my-first-repo.git
git push -u origin main
```

| Command | What it does |
|---|---|
| `git branch -M main` | Names your main branch `main` |
| `git remote add origin <url>` | Links your local repo to the GitHub repo |
| `git push -u origin main` | Uploads your commits to GitHub |

After the first time, you only need `git push`.

> **Sign-in note:** GitHub doesn't accept your account password for pushing. When asked to sign in, use the browser login that Git offers, or a personal access token from GitHub settings.

Refresh your GitHub page. Your files are online. 🎉

---

## 🔁 The Everyday Cycle

Once your repo is set up, this is what you repeat all the time:

```bash
git status                      # what changed?
git add .                       # stage the changes
git commit -m "Describe change" # save a snapshot
git push                        # upload to GitHub
```

---

## 🔍 Checking and Fixing

| What you want | Command |
|---|---|
| See which files changed and what is staged | `git status` |
| See a short list of your commits | `git log --oneline` |
| Unstage a file you staged by mistake | `git restore --staged file.txt` |
| Fix a typo in your last commit message (not pushed yet) | `git commit --amend -m "New message"` |

---

## 📥 Working With Existing Repositories

**Download a repo from GitHub (`clone`):**
```bash
git clone https://github.com/USERNAME/REPO-NAME.git
```

**Get the latest changes from GitHub (`pull`):**
```bash
git pull
```

---

## 🧰 Cheat Sheet

| Task | Command |
|---|---|
| Start a repo | `git init` |
| Check status | `git status` |
| Stage a file | `git add file.txt` |
| Stage everything | `git add .` |
| Save a snapshot | `git commit -m "message"` |
| Link to GitHub | `git remote add origin <url>` |
| Upload commits | `git push` |
| Download a repo | `git clone <url>` |
| Get latest changes | `git pull` |
| See history | `git log --oneline` |

---

## 🏋️ Practice Task

1. Create a folder called `git-practice` and run `git init`.
2. Add a `README.md` with your name and a one-line intro.
3. Stage it, commit it, and check `git log --oneline`.
4. Create a new repo on GitHub and push your project.
5. Add a second file, then repeat `add`, `commit`, and `push`.

✅ You're done when your GitHub page shows both files.