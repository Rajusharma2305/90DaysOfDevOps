Task 1: Multi-Job Workflow
What is a Job?

A job is a collection of steps that run on the same runner.

Example:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Building"

  test:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Testing"

Here there are 2 jobs.

Each job gets

its own virtual machine
its own filesystem
its own environment

That means Job 2 cannot automatically access files created in Job 1.

What is needs?

By default every job starts at the same time.

Example

build
test
deploy

All three run simultaneously.

But real projects require order.

Example

Build application
↓

Run tests
↓

Deploy

This is done using

needs:
Your workflow

Create

.github/workflows/multi-job.yml
name: Multi Job Workflow

on:
  workflow_dispatch:

jobs:

  build:
    runs-on: ubuntu-latest

    steps:
      - name: Build
        run: echo "Building the app"

  test:
    runs-on: ubuntu-latest

    needs: build

    steps:
      - name: Test
        run: echo "Running tests"

  deploy:
    runs-on: ubuntu-latest

    needs: test

    steps:
      - name: Deploy
        run: echo "Deploying"
What happens?
Start

↓

Build

↓

Test

↓

Deploy

If Build fails

Build ❌

Test skipped

Deploy skipped

If Test fails

Build ✅

Test ❌

Deploy skipped

This is why needs is used.

Workflow Graph

Go to

GitHub Repository

↓

Actions

↓

Open workflow

↓

Graph

You should see

Build
   │
   ▼
Test
   │
   ▼
Deploy
Task 2: Environment Variables

Environment variables store values that can be reused.

Instead of writing

myapp

myapp

myapp

everywhere,

store it once.

Three Levels

GitHub Actions allows variables at

Workflow level
Job level
Step level
Workflow Level

Accessible everywhere.

env:
  APP_NAME: myapp
Job Level

Accessible only inside that job.

jobs:

  build:

    env:
      ENVIRONMENT: staging
Step Level

Accessible only inside one step.

steps:

- name: Print

  env:
    VERSION: 1.0.0
Complete Workflow

Create

.github/workflows/environment.yml
name: Environment Variables

on:
  workflow_dispatch:

env:
  APP_NAME: myapp

jobs:

  demo:

    runs-on: ubuntu-latest

    env:
      ENVIRONMENT: staging

    steps:

      - name: Print Variables

        env:
          VERSION: 1.0.0

        run: |
          echo "App: $APP_NAME"
          echo "Environment: $ENVIRONMENT"
          echo "Version: $VERSION"

      - name: Print GitHub Context

        run: |
          echo "Commit SHA: ${{ github.sha }}"
          echo "Triggered by: ${{ github.actor }}"
Output
App: myapp

Environment: staging

Version: 1.0.0

Commit SHA:
63af98765bc....

Triggered by:
RajaVardhan
GitHub Context Variables

GitHub provides information about every workflow run.

Examples

github.actor

Who started workflow.

github.sha

Commit ID.

github.ref

Branch.

github.repository

Repository name.

github.workflow

Workflow name.

These are called contexts.

Task 3: Job Outputs

Suppose Job 1 calculates something.

Example

Today's Date

Version Number

Docker Image Tag

Build Number

How can Job 2 use it?

Using outputs.

Workflow

Create

.github/workflows/job-outputs.yml
name: Job Outputs

on:
  workflow_dispatch:

jobs:

  generate-date:

    runs-on: ubuntu-latest

    outputs:
      today: ${{ steps.date.outputs.today }}

    steps:

      - name: Get Date
        id: date

        run: |
          echo "today=$(date)" >> $GITHUB_OUTPUT

  print-date:

    runs-on: ubuntu-latest

    needs: generate-date

    steps:

      - name: Print Date

        run: |
          echo "Today's Date:"
          echo "${{ needs.generate-date.outputs.today }}"
How does it work?
Step 1
date

runs

date

Example output

Fri Jul 25
Step 2

Writes

today=Fri Jul 25

into

$GITHUB_OUTPUT
Step 3

Job exposes it

outputs:
Step 4

Next job reads

needs.generate-date.outputs.today
Why use outputs?

Real examples:

Build job creates Docker image tag.
Test job uses that image.
Deploy job uses the same image tag.
Build generates version number.
Release job uses version.
Terraform job outputs infrastructure ID.
Deployment job consumes it.

Outputs let one job pass data to another without recalculating it.

Task 4: Conditionals

GitHub lets you decide when jobs or steps should run using if:.

1. Run only on the main branch
- name: Main Branch

  if: github.ref == 'refs/heads/main'

  run: echo "Running on main"

If current branch is

main

Runs.

Otherwise skipped.

2. Run only when previous step failed
- name: Fail Step

  run: exit 1

- name: Run if Failed

  if: failure()

  run: echo "Previous step failed"

failure() checks whether an earlier step in the current job failed.

3. Run job only on push
jobs:

  push-job:

    if: github.event_name == 'push'

    runs-on: ubuntu-latest

    steps:

      - run: echo "Push event"

If event is

pull_request

Job is skipped.

4. continue-on-error
- name: Error Step

  continue-on-error: true

  run: exit 1

- name: Next Step

  run: echo "Still running"

Normally

Step 1 fails

Workflow stops

With

continue-on-error: true
Step 1 fails

↓

Workflow continues

↓

Next step executes

Useful for optional checks, experiments, or collecting diagnostics without failing the whole workflow.

Task 5: Smart Pipeline

Create

.github/workflows/smart-pipeline.yml
name: Smart Pipeline

on:
  push:

jobs:

  lint:
    runs-on: ubuntu-latest

    steps:
      - run: echo "Linting..."

  test:
    runs-on: ubuntu-latest

    steps:
      - run: echo "Running tests..."

  summary:
    runs-on: ubuntu-latest

    needs:
      - lint
      - test

    steps:

      - name: Branch Summary

        run: |
          if [[ "${{ github.ref }}" == "refs/heads/main" ]]; then
            echo "Main branch push"
          else
            echo "Feature branch push"
          fi

      - name: Commit Message

        run: |
          echo "${{ github.event.commits[0].message }}"
Workflow Execution
Push

      │

 ┌────┴─────┐
 │          │
 ▼          ▼

Lint      Test

 │          │

 └────┬─────┘
      ▼

Summary

Here lint and test run in parallel because neither has a needs dependency. The summary job waits for both using:
