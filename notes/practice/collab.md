# Collaborative Development on GitHub

- A useful video for reference: [Collaborative coding with Github (2025) by Eric Bezzam](https://www.youtube.com/watch?v=3PIcBzBj5jY)

---

## Demo

1. Create new repo on GitHub under the class's organization
   - e.g. https://github.com/vk-cs-foundations-fall-25/collab-demo

2. Add collaborators to the repo on the website (unless GitHub classroom has already configured it)

   - Note: can't configure branch protection because it seems to require a paid subscription

3. Each collaborator clones the repo (using PAT as password)
   
   Example commands:
   ```
   cd <collab1-github-dir>
   git clone https://github.com/vk-cs-foundations-fall-25/collab-demo.git
   cd collab-demo
   git config user.name <collab1-name>
   git config user.email <collab1-email>
   export PS1="<collab1-name>$ "
   ```

4. Create issues and assign to collaborators on the website

   Example issues:
   1. Define API and empty tests
   2. Implement method1
   3. Implement method2

5. Assignee defines API on a branch and creates a GitHub pull request to merge the branch into `main`
   
   Example commands:
   ```
   git checkout main
   git pull
   git checkout -b api
   git add .
   git commit -m "Fix #1: define API..."
   git push origin api
   ```

   - Create GitHub pull request on the website to pull changes from the api branch into the main branch
     - Assign another collaborator as the reviewer
     - Conduct code review
     - Merge after approval

6. Each collaborator follows the same workflow to address all issues

---

## Concepts

1. **GitHub Issue**
   - Project management
   - Tasks, bugs, ideas, etc.
   - Assigned to collaborators
1. **Git Branch**
   - Isolated line of development
   - One collaborator can create multiple branches, one for each "feature"
   - Facilitates code reviews on GitHub via GitHub Pull Requests (not to be confused with git pull)
1. **GitHub Pull Request**
   - Request to **merge** a branch into the main branch
   - **Code-review**
     - Improve code quality
     - Share implementation knowledge
   - After approval, merge commit
     - May require resolving conflicts

---

## Useful Commands

```
git clone <repo-url>              # Clone remote repo locally
git branch feature-name           # Create branch
git checkout -b feature-name      # Create and switch
git add .                         # Stage everything for commit
git commit -m "Fixes #3: ..."     # Commit on issue
git push origin feature-name      # Push feature-name to remote
git pull origin main              # Update main from remote
git merge main                    # Merge main into current
```

---