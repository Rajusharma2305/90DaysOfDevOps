Task 1: GitHub-Hosted Runners

Create:

name: Hosted Runners Demo

on:
  workflow_dispatch:

jobs:

  ubuntu-job:
    runs-on: ubuntu-latest
    steps:
      - name: Print Runner Info
        run: |
          echo "OS: Linux"
          hostname
          whoami

  windows-job:
    runs-on: windows-latest
    steps:
      - name: Print Runner Info
        shell: powershell
        run: |
          Write-Host "OS: Windows"
          hostname
          whoami

  macos-job:
    runs-on: macos-latest
    steps:
      - name: Print Runner Info
        run: |
          echo "OS: macOS"
          hostname
          whoami
Expected Result

All 3 jobs start simultaneously.

Example:

ubuntu-job     Running
windows-job    Running
macos-job      Running
Notes

What is a GitHub-hosted runner?

A temporary virtual machine provided by GitHub to execute workflow jobs.

Who manages it?

GitHub manages everything:

OS updates
Security patches
Installed software
Cleanup after job completion
Task 2: Explore Pre-installed Tools

Add another job:

  tools-check:
    runs-on: ubuntu-latest

    steps:
      - name: Check Installed Tools
        run: |
          docker --version
          python --version
          node --version
          git --version
Example Output
Docker version 28.x.x
Python 3.x.x
v22.x.x
git version 2.x.x
Notes

Why are pre-installed tools useful?

Because workflows run faster.

Without them:

Install Docker
Install Python
Install Node
Install Git

every workflow would waste several minutes.

With pre-installed tools:

Start workflow
Use tools immediately
Task 3: Setup Self-Hosted Runner

Go to:

Repository
 └── Settings
      └── Actions
           └── Runners
                └── New self-hosted runner

Choose:

Linux
x64

GitHub generates commands like:

mkdir actions-runner

cd actions-runner

curl -o actions-runner-linux-x64.tar.gz -L https://github.com/actions/runner/releases/download/...

tar xzf ./actions-runner-linux-x64.tar.gz

./config.sh --url https://github.com/USERNAME/REPO --token XXXXX

Start runner:

./run.sh

Permanent service:

sudo ./svc.sh install
sudo ./svc.sh start
Verify

GitHub should show:

Online ●
Idle

with a green dot.

Task 4: Run Workflow on Self-Hosted Runner

Create:

.github/workflows/self-hosted.yml

name: Self Hosted Runner

on:
  workflow_dispatch:

jobs:

  test-runner:
    runs-on: self-hosted

    steps:

      - name: Machine Details
        run: |
          hostname
          pwd
          whoami

      - name: Create File
        run: |
          echo "Hello from self hosted runner" > myfile.txt

      - name: Verify File
        run: |
          ls -l
Verify

SSH into your VM:

ls

Output:

myfile.txt

If present, the workflow really ran on your machine.

Task 5: Labels

Add label:

my-linux-runner

GitHub:

Settings
 → Actions
 → Runners
 → Your Runner
 → Labels

Update workflow:

runs-on:
  - self-hosted
  - my-linux-runner

or

runs-on: [self-hosted, my-linux-runner]
Why labels?

Imagine:

Runner 1 → Ubuntu
Runner 2 → Docker Server
Runner 3 → Production Server
Runner 4 → High Memory Server

Without labels:

runs-on: self-hosted

Job can run anywhere.

With labels:

runs-on: [self-hosted, docker]

Job only runs on Docker machine.

Task 6: GitHub Hosted vs Self Hosted
Feature	GitHub-Hosted	Self-Hosted
Who manages it?	GitHub	You
Cost	Free minutes + paid beyond limits	You pay for server
Pre-installed tools	Many tools already installed	You install/manage tools
Good for	Most CI/CD workloads	Custom environments, private infrastructure
Security concern	Code runs on GitHub VMs	You must secure the server
Maintenance	None	OS updates, patches, backups
Scalability	Automatic	You add servers manually
Interview Questions
What is a runner?

A runner is a machine that executes GitHub Actions jobs.

Difference between GitHub-hosted and self-hosted runners?

GitHub-hosted runners are managed by GitHub, while self-hosted runners are managed by the user.

Can multiple jobs run in parallel?

Yes. Jobs run in parallel by default unless dependencies are defined using needs.

What happens after a GitHub-hosted runner completes a job?

The VM is destroyed and a fresh VM is used for the next run.

Why use a self-hosted runner?
Access internal resources
Custom software
More CPU/RAM
Long-running workloads
Cost optimization at scale
