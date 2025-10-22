# Collaborative Development on GitHub

This is a very brief overview of how to collaboratively work on a project with others on GitHub.

Here's a useful video for reference: [Collaborative coding with Github (2025) by Eric Bezzam](https://www.youtube.com/watch?v=3PIcBzBj5jY)

---

## Demo

1. Create new repo on GitHub under the class's organization
  
   e.g. https://github.com/vk-cs-foundations-fall-25/collab-demo

   - Enable Issues
   - Enable Discussions

1. Add collaborators to the repo on the website (unless GitHub classroom has already configured it)

   - Note: can't configure branch protection because it seems to require a paid subscription

2. Each collaborator clones the repo (using PAT as password)
   
   Example commands:
   ```
   cd <collab1-github-dir>
   git clone https://github.com/vk-cs-foundations-fall-25/collab-demo.git
   cd collab-demo
   git config user.name <collab1-name>
   git config user.email <collab1-email>
   export PS1="<collab1-name>$ "
   ```

3. Create issues and assign to collaborators on the website

   Example issues:
   1. Define API and empty tests
   2. Implement method1
   3. Implement method2

4. Assignee defines API on a branch and creates a GitHub pull request to merge the branch into `main`
   
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

5. Each collaborator follows the same workflow to address all issues

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

## Best Practices

1. Branch Naming Conventions
   
   Use clear, descriptive names:
   - ⁠feature/user-authentication
   - bugfix/login-error
   - hotfix/security-patch
   - refactor/database-optimization

2. Commit Practices
  
   - Commit frequently with meaningful messages
   - Keep commits atomic: Each commit should represent one logical change
   - Write good commit messages:

      ```
      Add user authentication feature

      - Implement JWT token generation
      - Add login endpoint
      - Create user session middleware

      Closes #123
      ```

1. Keep Branches Up to Date

   Regularly merge or rebase from main:
   
   ```
   git checkout feature-login
   git merge main

   # Or for a cleaner history:
   git rebase main
   ```

1. Small, Focused Pull Requests

   - Easier to review
   - Faster to merge
   - Fewer conflicts	
   - Easier to roll back if needed

   Aim for:
   - < 400 lines of code changed
   - Single purpose or feature
   - Complete and tested

2. Communication
   
   - Comment on PRs actively
   - Use GitHub Discussions
   - Tag relevant people with @mentions
   - Update PR descriptions as changes are made