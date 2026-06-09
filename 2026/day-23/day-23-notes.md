🚀 Day 21 of My DevOps Journey – Git Branching, Remotes, Clone & Fork

Today I explored one of the most important Git concepts used in real-world software development and DevOps workflows: **Branches and Remote Repositories**.

🔹 Understanding Git Branches

Learned that a branch is an independent line of development that allows us to work on new features, bug fixes, or experiments without affecting the main codebase.

Key concepts:
✅ What is a branch?
✅ Why use branches instead of committing directly to main?
✅ What is HEAD in Git?
✅ What happens when switching between branches?

🔹 Hands-On Branching Practice

Worked with essential branching commands:

```bash
git branch
git branch feature-1
git switch feature-1
git switch -c feature-2
git branch -d feature-2
```

Learned the difference between:

• `git checkout` – older command with multiple purposes
• `git switch` – modern command focused on branch switching

🔹 Creating Independent Development History

✅ Created feature branches
✅ Made commits on feature branches
✅ Switched back to main and verified changes remained isolated
✅ Deleted unnecessary branches

This helped me understand how teams develop features independently before merging them.

🔹 Working with GitHub Remotes

Connected my local repository to GitHub and pushed multiple branches.

```bash
git remote add origin <repository-url>
git push -u origin main
git push -u origin feature-1
```

Learned:
• origin = my repository/fork
• upstream = original source repository

🔹 Pulling Changes from GitHub

Made changes directly on GitHub and synchronized them locally.

```bash
git fetch
git pull
```

Difference:
📌 git fetch downloads changes only
📌 git pull downloads and merges changes automatically

🔹 Clone vs Fork

Explored two common collaboration workflows:

Clone:
• Creates a local copy of a repository

Fork:
• Creates a personal copy of someone else's repository on GitHub

Use Clone when:
✅ You have direct access to contribute

Use Fork when:
✅ Contributing to open-source projects without write access

🔹 Key Takeaway

Modern software development is built around branches and collaboration. Instead of making all changes on the main branch, developers create feature branches, test changes safely, and then merge them back into the main codebase.

Workflow learned today:

Feature Branch → Commit Changes → Push to GitHub → Review → Merge

Every DevOps engineer should be comfortable with Git branching because CI/CD pipelines, pull requests, and team collaboration all depend on it.

#DevOps #Git #GitHub #VersionControl #Branching #OpenSource #Linux #CloudComputing #DevOpsEngineer #LearningInPublic #100DaysOfDevOps #SoftwareEngineering
