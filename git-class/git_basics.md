# Git & GitHub —

---

## What even is Git?

Git is a **save system for your code**.

Like in a video game where you save your progress — Git lets you save your code at any point, go back to old saves, and even work on multiple versions at the same time.

Without Git:
- You accidentally delete something → it's gone forever
- You try a new feature, break everything → no way back
- You work with a teammate → you keep overwriting each other's files

With Git:
- Every save is stored forever
- You can undo anything
- Teams can work on the same project without fighting

---

## What is GitHub?

GitHub is just a **website** that stores your Git history online.

Your computer has the code.
GitHub has a backup of it on the internet.
That's the whole relationship.

Git = the tool (lives on your computer)
GitHub = the website (lives on the internet)

---

## The 3 commands you already know — explained properly

### 1. `git init`
You run this once inside a folder. It basically says:
> "Hey Git, start tracking this folder."

Git creates a hidden `.git` folder inside. That's where it stores all your saves. Don't touch that folder.

```bash
mkdir my-project
cd my-project
git init
```

---

### 2. `git add`
You made some changes. Now you're telling Git:
> "These are the files I want to include in my next save."

```bash
git add .          # add everything
git add index.html # add just one file
```

Think of it like putting things in a box before sealing it.
`git add` = putting stuff in the box.

---

### 3. `git commit`
This actually saves it. You seal the box and label it.

```bash
git commit -m "added login page"
```

The message after `-m` is your label. Write something useful — future you will thank you.

Good messages:
- `"fixed navbar bug"`
- `"added user profile page"`
- `"removed unused files"`

Bad messages:
- `"asdfjkl"`
- `"fix"`
- `"idk"`

---

### 4. `git push`
Upload your saves to GitHub so it's backed up online.

```bash
git push origin main
```

`origin` = the GitHub repo (that's just the default name for it)
`main` = the branch you're pushing to (more on branches below)

---

## What is a Commit, really?

Every commit is a **snapshot** of your entire project at that moment.

```
v1 (first code) → v2 (added login) → v3 (fixed bug) → v4 (you are here)
```

You can go back to any of these snapshots anytime. Git stores the difference between each one, so it's super efficient.

To see all your commits:
```bash
git log
```

To go back to an old commit temporarily:
```bash
git checkout abc1234   # that weird number is the commit ID from git log
```

---

## Branches — the most important concept

### The problem without branches

Your app works perfectly. Boss says: add dark mode.
You start coding directly. You break something. Now the whole app is broken.
There's no "safe" version anymore.

### The solution: branches

A branch is a **copy of your code where you can experiment freely**.
Main stays safe. You work in your branch. If you mess up, just delete the branch. No damage.

```
main:    v1 → v2 → v3 ─────────────────→ v4 (merged!)
                    ↘                   ↗
feature:             f1 → f2 → f3 ──→
```

### How to use branches

```bash
# create a new branch and switch to it
git checkout -b dark-mode

# now you're on the dark-mode branch
# all commits go here, main is untouched

git add .
git commit -m "added dark mode"

# switch back to main
git checkout main

# bring your work into main
git merge dark-mode
```

### Golden rule at any job
> Nobody commits directly to main. Ever.
> Always make a branch. Always.

---

## Pull Requests (PR) — how teams work

At a company, you don't merge your own code into main.
You push your branch to GitHub, then open a **Pull Request**.

A PR is basically you saying:
> "Hey team, I wrote some code. Can someone check it before it goes live?"

### The flow

```
your branch → git push → open PR on GitHub → teammate reviews → approved → merged to main
```

### How to open a PR

```bash
# push your branch to GitHub
git push origin dark-mode
```

Then go to GitHub.com → your repo → you'll see a green button **"Compare & pull request"** → click it → write what you did → **Create pull request**.

Your teammate gets notified. They read your code, leave comments.
You fix stuff, push again — the PR updates automatically.
They approve → click Merge → your code is in main.

---

## Merge Conflicts — don't panic

A conflict happens when **two people edited the same line** of the same file.

```
You changed line 5 to:        background: black;
Your teammate changed line 5:  background: dark-gray;

Git doesn't know which one to keep. So it asks you.
```

Git will put this inside your file:

```
<<<<<<< HEAD (your code)
  background: black;
=======
  background: dark-gray;
>>>>>>> their branch
```

### How to fix it

1. Open the file
2. Decide which version to keep (or write a new combined version)
3. Delete all the `<<<<<<<`, `=======`, `>>>>>>>` marker lines
4. Save the file
5. Run:

```bash
git add .
git commit -m "resolved conflict"
```

Done. That's it.

---

## git clone — joining a project

You're new at a company. First day. You need to download the whole project.

```bash
git clone https://github.com/company/project.git
```

This downloads the entire repo to your laptop. You do this **once**.

---

## git pull — getting your teammate's updates

Your teammate pushed new code while you were working. You need their updates.

```bash
git pull origin main
```

**Do this every morning before you start working.**
Always pull before you push. Otherwise you might get conflicts.

---

## The real daily workflow at a job

This is what every developer does every single day:

```bash
# 1. morning — get latest code from team
git pull origin main

# 2. create your branch for today's task
git checkout -b feature/user-profile

# 3. ... write your code ...

# 4. save your work
git add .
git commit -m "added user profile page"

# 5. push your branch to GitHub
git push origin feature/user-profile

# 6. go to GitHub → open Pull Request
# 7. teammate reviews it
# 8. they approve → merge into main
# 9. your code is live 🎉
```

That's the full loop.

---

## Useful commands cheatsheet

| Command | What it does |
|---|---|
| `git init` | start tracking a folder |
| `git status` | see what files have changed |
| `git add .` | stage all changes |
| `git commit -m "msg"` | save a snapshot |
| `git log` | see all past commits |
| `git push origin main` | upload to GitHub |
| `git pull origin main` | download latest from GitHub |
| `git checkout -b name` | create and switch to new branch |
| `git checkout main` | switch back to main branch |
| `git merge branch-name` | bring branch into current branch |
| `git clone URL` | download a repo for the first time |
| `git diff` | see exactly what lines changed |

---

## What's inside the `.git` folder (bonus)

When you run `git init`, Git creates a hidden `.git` folder.
This is where all your history lives. Never delete it.

Inside `.git`:
- `objects/` — every version of every file you ever committed, stored as compressed snapshots
- `refs/` — pointers to your branches (a branch is literally just a file containing one commit ID)
- `HEAD` — a file that says "you are currently on this branch"
- `config` — settings for this repo

When you commit, Git:
1. Takes a snapshot of all your files
2. Compresses them
3. Gives the snapshot a unique ID (that long weird hash like `a3f9c2d`)
4. Stores it in `objects/`
5. Updates your branch pointer to point to this new commit

That's literally it. Git is just a very smart file storage system.

---

## Common beginner mistakes

**Committing directly to main**
Always branch. Even if you're working alone. Get into the habit.

**Never running git pull before working**
Always pull first. Saves you from 90% of conflicts.

**Vague commit messages**
Write what you actually did. You'll thank yourself in 3 months.

**Panicking at merge conflicts**
They look scary. They're not. Just pick which code to keep and remove the markers.

**Deleting the `.git` folder**
This deletes your entire history. Don't touch it.

---
