# Complete Walkthrough: GitHub Skills - Introduction to GitHub

This guide details the complete process of completing the **Introduction to GitHub** Skills course. It covers the concepts, Git commands, and GitHub workflows required to complete each step.

---

## Prerequisites
Before starting, ensure that you have:
* **Git** installed on your system.
* Your **GitHub repository** for the course cloned locally.
* Your Git CLI configured with your username and email:
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "your.email@example.com"
  ```

---

## Step 1: Create a Branch

A **branch** is a parallel version of your repository. By default, every repository starts with one branch named `main`. Creating branches allows you to safely develop new features or test changes without affecting the production/main codebase.

### Activity: Create `my-first-branch`
To start the course, you must create a branch named `my-first-branch`.

1. **Open your terminal** and navigate to your cloned repository folder.
2. **Create and switch to the new branch** using:
   ```bash
   git checkout -b my-first-branch
   ```
3. **Push the new branch** to GitHub to trigger the course workflow:
   ```bash
   git push -u origin my-first-branch
   ```

> [!NOTE]
> Pushing this branch triggers a GitHub Actions workflow (`1-create-a-branch.yml`) on your repository that updates `README.md` and the current step counter file (`.github/steps/-step.txt`) to Step 2.

4. **Pull the updates** back to your local repository:
   ```bash
   git fetch origin
   git checkout my-first-branch
   git pull origin my-first-branch
   ```

---

## Step 2: Commit a File

A **commit** represents a snapshot of your files at a specific point in time. When you make a commit, you write a short message explaining the changes you made.

### Activity: Add `PROFILE.md`
You need to add a file named `PROFILE.md` with some introductory text.

1. **Create the file** `PROFILE.md` in the root of your repository directory.
2. **Add the following content** inside `PROFILE.md`:
   ```markdown
   Welcome to my GitHub profile!
   ```
3. **Stage the file** for commit:
   ```bash
   git add PROFILE.md
   ```
4. **Commit the file** with a descriptive message:
   ```bash
   git commit -m "Add PROFILE.md"
   ```
5. **Push the commit** to GitHub:
   ```bash
   git push origin my-first-branch
   ```

> [!NOTE]
> Pushing this commit triggers the Step 2 workflow (`2-commit-a-file.yml`), which advances the instructions in `README.md` and updates the step counter to Step 3.

6. **Pull the updates** from origin:
   ```bash
   git fetch origin
   git pull origin my-first-branch
   ```

---

## Step 3: Open a Pull Request

A **pull request (PR)** is a proposal to merge changes from one branch into another. This is where code review, collaboration, and discussion happen.

### Activity: Create the Pull Request
You can open a pull request on the GitHub website or via the GitHub CLI.

#### Option A: Using the GitHub Web Interface (Recommended)
1. Navigate to your repository page on [GitHub](https://github.com).
2. Click the green **Compare & pull request** button at the top of the page.
3. Verify that `base: main` is selected as the destination and `compare: my-first-branch` is the source branch.
4. Set the title to `Add my first file`.
5. Click **Create pull request**.

#### Option B: Using GitHub REST API (Programmatic)
If you are developing a tool or script to automate this, you can send a POST request to the GitHub API:
```bash
curl -X POST \
  -H "Authorization: token YOUR_PERSONAL_ACCESS_TOKEN" \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/YOUR_USERNAME/skills-introduction-to-github/pulls \
  -d '{"title":"Add my first file","head":"my-first-branch","base":"main","body":"Create PROFILE.md"}'
```

> [!NOTE]
> Opening the PR triggers the Step 3 workflow (`3-open-a-pull-request.yml`), which advances the course instructions on the branch to Step 4.

6. **Pull the updates** to your local branch:
   ```bash
   git fetch origin
   git pull origin my-first-branch
   ```

---

## Step 4: Merge Your Pull Request

**Merging** combines the commits from your branch into the target branch (`main`).

### Activity: Merge and Clean Up

#### Option A: Using the GitHub Web Interface
1. Go to your pull request on GitHub.
2. Wait for the green **Merge pull request** button to become active.
3. Click **Merge pull request** and then **Confirm merge**.
4. Click **Delete branch** to clean up the branch on the remote repository.

#### Option B: Using GitHub REST API (Programmatic)
1. **Merge the PR** (replace `{pull_number}` with the PR ID, e.g., `3`):
   ```bash
   curl -X PUT \
     -H "Authorization: token YOUR_PERSONAL_ACCESS_TOKEN" \
     -H "Accept: application/vnd.github.v3+json" \
     https://api.github.com/repos/YOUR_USERNAME/skills-introduction-to-github/pulls/{pull_number}/merge \
     -d '{"commit_title":"Merge pull request","merge_method":"merge"}'
   ```
2. **Delete the remote branch**:
   ```bash
   curl -X DELETE \
     -H "Authorization: token YOUR_PERSONAL_ACCESS_TOKEN" \
     -H "Accept: application/vnd.github.v3+json" \
     https://api.github.com/repos/YOUR_USERNAME/skills-introduction-to-github/git/refs/heads/my-first-branch
   ```

---

## Step X: Wrap Up

Once the pull request is merged, a final push event is sent to the `main` branch. This triggers the workflow `4-merge-your-pull-request.yml`, which updates your `README.md` to show the final **Finish** step!

To wrap up locally:
1. **Switch to main**:
   ```bash
   git checkout main
   ```
2. **Pull the merged codebase**:
   ```bash
   git pull origin main
   ```
3. **Delete your local branch**:
   ```bash
   git branch -d my-first-branch
   ```

🎉 **Congratulations! You have completed the Introduction to GitHub Skills course.**
