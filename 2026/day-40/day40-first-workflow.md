Task 1: Setup Repository
Step 1: Create a GitHub Repository

Repository name:

github-actions-practice

Make it Public.

Step 2: Clone Repository
git clone https://github.com/<your-username>/github-actions-practice.git

cd github-actions-practice
Step 3: Create Workflow Folder Structure

Linux/Mac:

mkdir -p .github/workflows

Windows:

mkdir .github
mkdir .github\workflows

Your structure should look like:

github-actions-practice/
└── .github/
    └── workflows/
Task 2: Create Your First Workflow

Inside .github/workflows

Create:

hello.yml
hello.yml
name: First Workflow

on:
  push:

jobs:
  greet:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Print Message
        run: echo "Hello from GitHub Actions!"
What Happens?

When you push code:

Push Code
    ↓
GitHub Detects Push
    ↓
Starts Ubuntu VM
    ↓
Checks Out Repository
    ↓
Runs echo Command
    ↓
Pipeline Success
Commit and Push
git add .

git commit -m "first workflow"

git push origin main
Verify

Open GitHub

Repository
   ↓
Actions Tab

You should see:

✓ First Workflow

Green color means success.

Task 3: Understand Workflow Anatomy
name:

Workflow name shown in GitHub Actions.

name: First Workflow

Displayed as:

First Workflow

in Actions tab.

on:

Defines when workflow runs.

on:
  push:

Meaning:

Whenever code is pushed
run this workflow

Other examples:

on:
  pull_request:
on:
  workflow_dispatch:

Manual trigger button.

jobs:

Collection of work.

jobs:

Think:

Workflow
 └── Jobs

Example:

jobs:
  build:
  test:
  deploy:
runs-on:

Runner Operating System.

runs-on: ubuntu-latest

GitHub creates:

Fresh Ubuntu Machine

for every run.

steps:

Tasks executed inside a job.

steps:

Example:

steps:
  - checkout
  - build
  - test

Executed one after another.

uses:

Uses an existing GitHub Action.

uses: actions/checkout@v4

Meaning:

Download repository code
to runner machine

Without checkout:

ls

shows almost nothing because repo isn't downloaded.

run:

Runs shell commands.

run: echo "Hello"

Equivalent to:

echo "Hello"

on Ubuntu.

Step Name
- name: Print Message

Shown in logs.

Without it:

Step 1
Step 2

With it:

Checkout Code
Print Message

Much easier to debug.

Task 4: Add More Steps

Replace workflow with:

name: First Workflow

on:
  push:

jobs:
  greet:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Print Message
        run: echo "Hello from GitHub Actions!"

      - name: Print Date
        run: date

      - name: Print Branch Name
        run: echo ${{ github.ref_name }}

      - name: List Files
        run: ls -la

      - name: Print OS
        run: uname -a
Expected Output
Date
Mon Jun 22 ...
Branch
main

or

master
Files
.github
README.md
OS
Linux runner ...

Push Again

git add .

git commit -m "added more steps"

git push origin main

Watch a new workflow run.

Task 5: Break It On Purpose

Add:

- name: Fail Step
  run: exit 1

Example:

steps:
  - name: Checkout
    uses: actions/checkout@v4

  - name: Fail Step
    run: exit 1

Push:

git add .

git commit -m "break pipeline"

git push origin main
What Happens?
Checkout ✓

Fail Step ✗

Workflow Failed

Actions tab becomes:

🔴 Failed

instead of:

🟢 Success
Another Way

Misspell command:

run: echho "hello"

Output:

echho: command not found

Pipeline fails.

How To Read Errors

Click:

Actions
  ↓
Workflow Run
  ↓
Job
  ↓
Failed Step

Look for:

Error
Failed
Exit code
Command not found

Example:

Process completed with exit code 1

This means a command returned failure.

Final Learning Goal

By the end of today you should understand:

✅ What triggers a workflow (on:)

✅ What a job is (jobs:)

✅ What a runner is (runs-on:)

✅ What steps are (steps:)

✅ Difference between uses: and run:

✅ How to read GitHub Actions logs

✅ How a successful pipeline looks

✅ How a failed pipeline looks

After completing this, you'll be ready to build real CI pipelines (Build → Test → Docker Build → Deploy) in the next steps.
