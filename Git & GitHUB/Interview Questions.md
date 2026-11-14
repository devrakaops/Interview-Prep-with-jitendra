### 1. What is Version Control, and why do we use it?

**Answer:** Version Control is a system that records changes to a file or set of files over time so that you can recall specific versions later. We use it to track code history, collaborate with a team without overwriting each other's work, and revert back to a working state if something breaks.

---

### 2. What is the difference between Git and GitHub?

**Answer:**

* **Git** is a distributed version control tool installed locally on your computer to track changes in your code.
* **GitHub** is a cloud-based hosting service that lets you manage Git repositories online, collaborate with others, and back up your code.

---

### 3. What is a Git Repository?

**Answer:** A Git repository (or repo) is a folder or directory where Git tracks all the files and their complete change history. It contains a hidden `.git` folder that stores all the metadata and version history.

---

### 4. How do you initialize a new Git repository?

**Answer:** You use the `git init` command inside your project folder. This creates a hidden `.git` directory and starts tracking the project.

---

### 5. What are the three main states (areas) of files in Git?

**Answer:**

1. **Working Directory:** Where you actively modify, add, or delete files.
2. **Staging Area (Index):** Where you prepare and group changes before committing them.
3. **Local Repository:** Where Git permanently stores your committed snapshots.

---

### 6. What is the difference between `git add` and `git commit`?

**Answer:**

* `git add <file>` (or `git add .`) moves changes from the Working Directory to the Staging Area.
* `git commit -m "message"` takes the staged changes and permanently saves them as a new snapshot in your Local Repository.

---

### 7. How do you check the current status of your Git repository?

**Answer:** You use the `git status` command. It shows which files are modified, which files are staged for the next commit, and which files are untracked by Git.

---

### 8. What is the difference between `git clone` and `git pull`?

**Answer:**

* `git clone <url>` is used once to download an entire remote repository to your local computer for the first time.
* `git pull` is used on an existing local repository to fetch and merge the latest changes from the remote repository.

---

### 9. What is the difference between `git fetch` and `git pull`?

**Answer:**

* `git fetch` downloads new changes from the remote repository to your local machine, but it does **not** merge them into your current working files.
* `git pull` does both: it fetches the changes and immediately merges them into your active branch (`git fetch` + `git merge`).

---

### 10. What is a branch in Git, and why is it used?

**Answer:** A branch is an independent line of development. It allows you to work on new features or bug fixes in isolation without affecting the main production code (usually the `main` or `master` branch).

---

### 11. How do you create a new branch and switch to it?

**Answer:** You can create and switch to a new branch in one command using:

* `git checkout -b <branch-name>`
* Or using the newer command: `git switch -c <branch-name>`

---

### 12. What is `git merge`?

**Answer:** `git merge <branch-name>` combines the changes from one branch into your currently active branch. For example, merging a completed feature branch back into the `main` branch.

---

### 13. What is a Merge Conflict, and how do you resolve it?

**Answer:** A merge conflict happens when two branches modify the exact same line in a file, and Git does not know which change to keep. To resolve it:

1. Open the conflicted file and look for the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
2. Edit the file to keep the desired code and remove the markers.
3. Run `git add <file>` and `git commit` to finish the merge.

---

### 14. What does `git push` do?

**Answer:** `git push origin <branch-name>` uploads your local repository commits to a remote repository (like GitHub) so others can see and access your changes.

---

### 15. How do you view the commit history in Git?

**Answer:** You use the `git log` command. It lists all previous commits in reverse chronological order along with the commit hash, author, date, and commit message. (Tip: `git log --oneline` gives a clean, compact view).

---

### 16. What is a `.gitignore` file?

**Answer:** `.gitignore` is a plain text file where you list files or folders (like `node_modules/`, `.env`, or log files) that you want Git to ignore and never track or push to GitHub.

---

### 17. What is a Pull Request (PR) on GitHub?

**Answer:** A Pull Request is a GitHub feature used to propose changes from your branch to another branch (like `main`). It allows team members to review your code, discuss improvements, and approve the changes before merging.

---

### 18. What is the difference between Forking and Cloning on GitHub?

**Answer:**

* **Forking** creates a personal copy of someone else's repository under your own GitHub account (on the cloud).
* **Cloning** downloads a repository from GitHub onto your local computer.

---

### 19. What is `git stash` used for?

**Answer:** `git stash` temporarily saves your uncommitted changes and cleans your working directory so you can switch branches or pull updates without committing unfinished work. You can bring those changes back later using `git stash pop`.

---

### 20. What is the difference between `git revert` and `git reset`?

**Answer:**

* `git revert <commit-id>` undoes a previous commit by creating a **new commit** that reverses the changes. It is safe for shared branches because it preserves history.
* `git reset` moves the branch pointer backward and deletes commits from history. It is generally used only for local, unpushed changes.

---

### 21. What is the difference between Global and Local Git configuration? How do you set them?

**Answer:**

* **Local configuration** applies only to a single, specific repository (stored in `.git/config`).
* **Global configuration** applies to all repositories for your user account on your computer (stored in `~/.gitconfig`).
* **Commands:**
* Set global username/email: `git config --global user.name "Your Name"` and `git config --global user.email "you@example.com"`
* Set local username/email: Run the same commands without `--global` inside the project folder.



---

### 22. How do you check, add, or change the remote repository URL in Git?

**Answer:** A remote is a connection to your repository hosted on GitHub (usually named `origin`).

* **Check remote URL:** `git remote -v`
* **Add a new remote:** `git remote add origin <repository-url>`
* **Change an existing remote URL:** `git remote set-url origin <new-repository-url>`

---

### 23. What actually happens behind the scenes when you run `git init` vs `git clone`?

**Answer:**

* **`git init`** turns an existing local folder into a brand-new Git repository by creating a hidden `.git` folder. It starts with an empty commit history and has no connection to GitHub until you manually add a remote.
* **`git clone <url>`** automatically creates a new folder, runs `git init` inside it, connects it to the remote URL as `origin`, and downloads all files, branches, and complete commit history from GitHub.

---

### 24. What is the conceptual difference between the `main` branch and other feature branches?

**Answer:**

* The **`main` (or `master`) branch** represents the official, stable, and production-ready version of the project. Code in `main` should always work properly.
* **Other branches (like `feature/login` or `bugfix/header`)** are temporary, isolated workspaces created from `main`. Developers build and test new features in these branches so they do not accidentally break the live code in `main`.

---

### 25. What is the complete workflow of creating a Pull Request (PR) and merging it on GitHub?

**Answer:**

1. Create a new branch locally (`git checkout -b feature-branch`), make changes, and commit them.
2. Push the branch to GitHub (`git push origin feature-branch`).
3. Go to GitHub and click **Compare & pull request** to open a Pull Request from `feature-branch` into `main`.
4. Team members review the code, leave comments, and approve the PR.
5. Click **Merge pull request** on GitHub to combine your code into `main`, then safely delete the temporary `feature-branch`.

---

### 26. How do you list all branches, rename a branch, and delete a branch in Git?

**Answer:**

* **List local branches:** `git branch` (use `git branch -a` to see remote branches too)
* **Rename current branch:** `git branch -m <new-branch-name>`
* **Delete a merged branch locally:** `git branch -d <branch-name>` (use `-D` to force delete an unmerged branch)

---

### 27. What is `HEAD` in Git?

**Answer:** `HEAD` is a special pointer that tells Git which branch or commit you are currently working on. Normally, `HEAD` points to the latest commit of your currently checked-out branch. When you switch branches, `HEAD` moves to the new branch.

---
