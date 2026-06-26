Task 1: Pull Request Trigger

Create:

# .github/workflows/pr-check.yml

name: PR Check

on:
  pull_request:
    branches:
      - main

jobs:
  pr-validation:
    runs-on: ubuntu-latest

    steps:
      - name: Print PR branch
        run: echo "PR check running for branch: ${{ github.head_ref }}"
Test
git checkout -b feature-branch

Make a change:

echo "test" >> test.txt
git add .
git commit -m "PR test"
git push origin feature-branch

Open a Pull Request → main.

Verify

Go to:

Pull Request
↓
Checks

You should see:

PR Check
✓ Passed
Task 2: Scheduled Trigger

Create:

name: Daily Schedule

on:
  schedule:
    - cron: '0 0 * * *'

jobs:
  schedule-job:
    runs-on: ubuntu-latest

    steps:
      - run: echo "Running scheduled workflow"
Meaning
0 0 * * *
│ │ │ │ │
│ │ │ │ └─ Day of Week
│ │ │ └── Month
│ │ └── Day of Month
│ └──── Hour
└────── Minute

Runs:

Every day
00:00 UTC
Cron Expression Answer

Every Monday at 9 AM UTC:

0 9 * * 1
Task 3: Manual Trigger

Create:

# .github/workflows/manual.yml

name: Manual Deployment

on:
  workflow_dispatch:
    inputs:
      environment:
        description: "Deployment Environment"
        required: true
        default: "staging"

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Print Environment
        run: echo "Environment = ${{ github.event.inputs.environment }}"
Run

Actions → Manual Deployment

Click:

Run Workflow

Enter:

production

Output:

Environment = production
Task 4: Matrix Builds

Create:

# .github/workflows/matrix.yml

name: Matrix Build

on:
  workflow_dispatch:

jobs:
  test:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        python-version:
          - "3.10"
          - "3.11"
          - "3.12"

    steps:
      - uses: actions/checkout@v4

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python-version }}

      - name: Show Version
        run: python --version
Result

Runs 3 jobs in parallel:

Python 3.10
Python 3.11
Python 3.12
Extend Matrix with Operating Systems
strategy:
  matrix:
    os:
      - ubuntu-latest
      - windows-latest

    python-version:
      - "3.10"
      - "3.11"
      - "3.12"

runs-on: ${{ matrix.os }}
Total Jobs
2 OS × 3 Python Versions
= 6 Jobs
OS	Python
Ubuntu	3.10
Ubuntu	3.11
Ubuntu	3.12
Windows	3.10
Windows	3.11
Windows	3.12
Task 5: Exclude & Fail-Fast
name: Matrix Advanced

on:
  workflow_dispatch:

jobs:
  test:
    runs-on: ${{ matrix.os }}

    strategy:
      fail-fast: false

      matrix:
        os:
          - ubuntu-latest
          - windows-latest

        python-version:
          - "3.10"
          - "3.11"
          - "3.12"

        exclude:
          - os: windows-latest
            python-version: "3.10"

    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python-version }}

      - name: Show Version
        run: python --version

      - name: Simulate Failure
        if: matrix.python-version == '3.11'
        run: exit 1
How Many Jobs Run?

Original:

2 × 3 = 6

Excluded:

Windows + Python 3.10

Final:

5 jobs
fail-fast: true (Default)

If one matrix job fails:

Remaining running jobs are cancelled.

Example:

Job 1 ❌
Job 2 Cancelled
Job 3 Cancelled
Job 4 Cancelled

Useful when:

You want quick feedback.
