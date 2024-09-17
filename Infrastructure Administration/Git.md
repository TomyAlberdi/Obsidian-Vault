Created: 2024-09-17 16:23
## Family Tree:
1. Computer
2. [[Infrastructure Administration]]
-- -
## Introduction:

During the development of applications, whether web or mobile, we always encounter two imperative needs:
1. Having a continuously updated backup of our files.
2. The ability to share our code with other team members.

Git is a version control Software designed for the efficiency and reliability of maintaining applications when they have a large number of source code files. Its purpose is to keep track of file changes and coordinate the work that several people perform on the same files. In short, with Git, you can have a complete version history of a single file without the need to create multiple copies, allowing you to have all changes recorded and even revert to previous versions whenever you want. Additionally, with Git, you can easily share your files and track them to know which team member made specific modifications.
### Creating a local repository:

In the Bash terminal, you should navigate to the folder where you want to create the repository and use the command `git init`. This will create a local repository in the folder you are located in. Initially, this repository will be empty as no files have been added to it yet. This will be covered later. A repository, whether local or remote, is a storage for files. Here, files will be stored in small packages called commits. These packages allow tracking changes made, as each one has a timestamp (creation date) and an author. Commits will be our change history for the project, and this is why before doing anything, you need to tell this repository how to identify you. This is done by writing `git config user.name "my-username"`, replacing `my-username` with your GitHub username, in the folder where the repository is initialized. To confirm that your username is configured correctly, you can write the command `git config user.name`, and the terminal will return your username. Additionally, Git requires you to configure the email address linked to your account. This can be done with the command `git config user.email "your-email"`. It can be confirmed in the same way as your username.
### Adding files to the repository:

If you use the command `git status` in a repository with files that have not been added to it, the terminal will return a message informing you that these files are not part of the repository, so you should add them. To do this, use the command `git add filename`. You can use the command `git add .` to add all the files in the folder to the repository. When a file that is already added to the repository is modified, Git assumes that the file is new, so it will not be tracked in the repository. Therefore, you need to use `git add` again to re-add them.
### Confirming files:

When working with files, we are used to them being saved automatically or by asking the program to save them (Ctrl + S). Confirming modifications in Git is extremely important as it allows us to establish a checkpoint. As we have seen, a commit is a confirmation through which we tell the repository that the files we have been adding (one or several) are desired as a small package of additions or modifications that will have a timestamp and be signed by an author. Commits generate chronological points in the project's timeline that allow us to identify its state up to that specific moment and, in turn, go back to those points if necessary. This is done after adding the files to the repository (`git add`) with the command `git commit -m "message"`. Instead of "message," you should write, in a concise manner, the work done up to that point. This helps to know what modifications were made to the files without having to review them. The command `git log` will show us the history of commits made in this repository.