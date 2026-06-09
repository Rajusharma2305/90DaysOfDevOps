Task 1: Install and Configure Git
Verify Git Installation
git --version
Configure Git Identity
git config --global user.name "Raja Vardhan"
git config --global user.email "vardhanraja2305@gmail.com"
Verify Configuration
git config --list
Task 2: Create Your Git Project
Create Project Directory
mkdir devops-git-practice
cd devops-git-practice
Initialize Git Repository
git init
Check Repository Status
git status
Explore the .git Directory

Linux/macOS:

ls -la .git

Windows PowerShell:

dir .git -Force

Observe folders such as:

objects/
refs/
hooks/
logs/
HEAD
config
Task 3: Create Git Commands Reference

Create a file:

touch git-commands.md

Add the following content:

Git Commands Reference
Setup & Config
git --version

Shows installed Git version.

Example:

git --version
git config --global user.name

Sets Git username.

Example:

git config --global user.name "Raja Vardhan"
git config --global user.email

Sets Git email.

Example:

git config --global user.email "example@gmail.com"
Basic Workflow
git init

Creates a new Git repository.

Example:

git init
git add

Adds files to staging area.

Example:

git add git-commands.md
git commit

Creates a snapshot of staged changes.

Example:

git commit -m "Initial commit"
Viewing Changes
git status

Shows repository status.

Example:

git status
git log

Displays commit history.

Example:

git log
Task 4: Stage and Commit
Stage File
git add git-commands.md
Verify Staged Files
git status
Create First Commit
git commit -m "Add Git commands reference"
View Commit History
git log
Task 5: Build Commit History
Add More Commands

Update git-commands.md with:

git diff
git log --oneline
git restore
git rm
Check Changes
git diff
Commit #2
git add .
git commit -m "Add Git viewing commands"
Add More Notes

Update file again.

Commit #3
git add .
git commit -m "Add Git workflow commands"
Commit #4
git add .
git commit -m "Expand Git command reference"
Compact History
git log --oneline
