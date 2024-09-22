Created: 2024-09-17 16:23
## Family Tree:
1. Computer
2. [[Infrastructure Administration]]
-- -
GitHub is a place where programming projects are hosted for free, with the only requirement being to have an account.
### Repository:
A place where the files of your project will be stored and through which you can track them. It is important to note that a project corresponds to a repository. Repositories hosted on GitHub are called remote repositories. In parallel, each person on your team will have a copy of that repository on their computer, which we call local repositories. For Git to work correctly, it is necessary to create a link between local and remote so that you can keep backups of your local files connected with that place in the cloud.
### Branch:
A Git branch will allow us to work on versions of our files in a much more organized way. So far, we have seen that the repository we created with Git or cloned from GitHub has a default root called main, in which we save the versions of our work every time we make a commit. In the projects we will carry out as developers, all the changes we make in a repository must be shared with a team. That team will be responsible for approving our modifications. So, when we work on new features, need to fix errors, or simply want to better organize our files, we should do it in a separate space until our team approves those changes. Branches are used for this purpose. A branch will function as a workspace just for us, where we can save our changes and run all the necessary tests until we are sure to share those changes.
#### Creating Branches:
It is important to understand that a branch is just a line of development that is based on the repository but does not directly act on it, meaning it does not modify it. We start with a repository that looks like this:
To create a new branch, we use the command `git branch`. This command allows us to create, list, rename, and delete branches. It does not allow switching between branches or merging a forked history.
- `git branch`: Lists all branches in your repository. Similar to `git branch --list`.
- `git branch <branch>`: Creates a new branch called `<branch>`.
- `git branch -d <branch>`: Deletes the branch called `<branch>`. Git prevents us from deleting the branch if it has changes that have not yet been merged with the main branch.
- `git branch -D <branch>`: Forces the deletion of the specified branch, even if it has unmerged changes.
#### Git Checkout:
To move from one branch to another, execute the command `git checkout <branch_name>`. Generally, Git will only allow us to move to another branch if we have no changes. If we have changes, to switch branches we should:
- Discard them (undo the changes).
- Confirm them (make a commit).
#### Save changes and upload them to the remote repository: 
Once we finish making the changes we want in our branch, we execute the same commands we have seen so far: `git add`, `git commit`, `git status`, and `git log`. But when we want to upload these changes, we must use `git push` with the name of the branch we are on: `git push origin <branch>`. Similarly, to fetch the changes from that branch, use `git pull` adding from where you want to fetch the changes: `git pull origin <branch>`.
## Cheat Sheet

| Command                                                               | Usage                      |
| --------------------------------------------------------------------- | -------------------------- |
| `git remote set-url origin https://token@github.com/user/project.git` | Change origin URL or Token |
| `git log -1 --pretty=%B`                                              | Get last commit message    |
| `git reset --soft HEAD~`                                              | Cancel last commit         |
