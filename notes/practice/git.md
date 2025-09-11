# Git

- A popular version control system (VCS)

- Used in GitHub

- What is a VCS?

  - You've likely seen revision history of a file in Google Drive or OneDrive

  

  ![](../media/vcs-file.excalidraw.svg)

  

  - VCS is an enhanced version (no pun intended) of that
  - Instead of maintaining separate versions of each file, a VCS mantains versions of the entire set of files
    - When you change a set of files and *commit* the changes, the set of changes is assigned a version number and maintained by the VCS in the version history



​		![](../media/vcs-repo.excalidraw.svg)

- Why use a VCS?
  - Misconception: VCS is just for teams
  - Single user
    - Revert to a previous version if you mess up 
    - Create *branches* (more in this later) to try out new features/ideas without affecting the main content
    - Maintain documenation of changes
  - Collaboration/Team
    - Parallel development without overwriting each other's changes
    - Track changes by person (accountability, troubleshooting)
    - Code reviews
    - Access control
- The core workflow to work on a GitHub repo is the following:
  1. Use `git clone` to clone the remote repo (on GitHub) to your local system (thereby creating a local repo)
  2. Use your chosen editors/IDEs to make changes locally to your local repo
  3. Use `git commit` to commit changes locally to your local repo
  4. Use `git push` to push commits from your local repo to the remote repo on GitHub

​		![](../media/git-workflow.excalidraw.svg)

​	

- Use git on the commandline for pedagogy for now
  - Later you can use git integrations with your IDE (e.g. in VSCode)
- Reference: https://education.github.com/git-cheat-sheet-education.pdf

## Core Workflow

1. Make sure [Git](https://git-scm.com/) is installed on your computer

   `git -version`

2. Clone the remote repo to your local system using terminal commands

   ```bash
   export REPOS_DIR="github"
   export REMOTE_REPO="https://github.com/vishesh-khemani/hello-git.git"
   export REPO_NAME="hello-git"
   
   mkdir REPOS_DIR
   cd REPOS_DIR
   git clone $REMOTE_REPO
   cd $REPO_NAME
   ```

   - Choose your own REPOS_DIR
   - Copy the REMOTE_REPO from GitHub
     - Click the green "Code" button and copy the URL (either HTTPS or SSH).
   - You may need authentication if the repo is private

3. Make changes to your local repo

4. Check on the status of changes in your local repo

   `git status`

5. Select files to stage for a commit
   1. Subset of files
      - `git add <file>`
   2. All modified/deleted files
      - `git add .`
   3. All new/modified/deleted files
      - `git add -A`
6. Commit staged files to your local repo
   - `git commit`
   - Use a concise and clear commit message
     - Serves as documentation of changes, especially when collaborating
   - Note: the changes are only committed to the local repo, not to the remote repo
7. Push the local commits to the remote repo
   - `git push`
8. Check on GitHub that your commits were indeed pushed

## Branching

- Can create separate **branches** within a **repo**
- Each branch contains commits for an independent line of development
- Why branch?
  - Work on different features/bugs independently (without affecting the main branch and other collaborators)
  - Experiment with new ideas safely
  - "Cut a release branch" from the main branch to deploy



​	![](../media/git-branching.excalidraw.svg)

- Commands
  - Switch to the `main` branch
    - `git checkout main`
  - Create the `feature1` branch and switch to it
    - `git checkout -b feature1`
    - Develop feature1 and add a commit for each milestone
  - Need to fix a bug on the main branch
    - `git checkout main`
    - `git checkout -b bugfix1`
    - Fix the bug and commit the fix
    - Merge the fix back to the main branch and delete the bugfix branch
      - `git checkout main`
      - `git merge bugfix1`
      - `git branch -d bugfix1`
  - Finish developing feature1 and merge it back to main
    - `git checkout main`
    - `git merge feature1`
    - `git branch -d feature1`
- Remember that the commits and merges are only on the local repo and you have to use `git push` to push the commits to the remote repo