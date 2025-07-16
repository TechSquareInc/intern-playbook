# 🔁 Getting Started with Git

*Git is a version control system that helps you track changes in code, collaborate with others, and manage different versions of a project. This guide introduces the core concepts and basic commands to get you started with Git.*

---

## What is Version Control? 

Version control allows you to:
- Track the history of changes to files
- Revert to previous versions if something breaks
- Work on new features or fixes without affecting the main project
- Collaborate with others without overwriting each other's work

Git is a distributed [version control](https://www.atlassian.com/git/tutorials/what-is-version-control) system, meaning every user has a complete copy of the project history.

## Installing Git
```bash
sudo apt update
sudo apt install git
```

## Basic Git Workflow

1. **Initialize a repository**
- Turns a directory into a Git repository
```bash
git init
```
2. **Check repository status**
- Allows you to monitor changes made since your last commit
```bash
git status
```
3. **Add files to a staging area**
- Add changes to a your staging area that are ready to be included in your next commit
```bash
git add filename
git add . # Adds all files in the directory
git add -p # Sorts through changes to add one by one
```
4. **Commit changes**
- Create a permanent snapshot of your changes in your local repository
```bash
git commit -m "Describe what you changed or added"
```
5. **View commit history**
- Shows a list of commits made in reverse chronological order
```bash
git log
```

## Connecting to a Remote Repository
To collaborate with others, you'll typically push your code to a platform like GitHub, GitLab, or Bitbucket.

### Add a remote repository
```bash
git remote add origin https://github.com/yourusername/your-repo.git
```
### Push your code
```bash
git push -u origin main
```
- The `-u` (upstream) links your local branch to a remote repository.

## Branching and Merging

### Creating a new branch
```bash
git checkout -b branch-name
```
### Switch branches
```bash
git checkout branch-name
```
### Merge a branch
```bash
git merge branch-name
```
### Delete a branch
```bash
git branch -d branch-name
```

## Clonig a Repository
To download a remote project and work on it:
```bash
git clone https://github.com/username/project.git
```

## .gitignore File
Use a `.gitignore` file to exclude files or directories from being tracked by Git.

**Example:**
```bash
*.log
.env
__pycache__/
node_modules/
```

## Undoing Changes
- Unstage a file
```bash
git reset HEAD filename
```
- Discard changes in a file
```bash
git checkout -- filename
```
- Revert a commit
```bash
git revert <commit-id>
```

## Resources
- [GitHub Learning Lab](https://github.com/apps/github-learning-lab): bot lead series of practical projects to level up your GitHub skills
- [Git Branching](https://learngitbranching.js.org/?locale=en_US): a visual and interactive way to learn Git on the web
- [Git Book (free)](https://git-scm.com/book/en/v2): a free complete and indepth Git resource
- [Git Cheatsheet (GitHub)](https://education.github.com/git-cheat-sheet-education.pdf): features the most important and commonly used Git commands for easy reference.
- [Git-it](https://github.com/jlord/git-it-electron): a desktop app that teaches you how to use Git and GitHub on the command line.
