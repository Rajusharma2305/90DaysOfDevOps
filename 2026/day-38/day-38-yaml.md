Task 1: Key-Value Pairs

person.yaml

name: Raja Vardhan
role: DevOps Engineer
experience_years: 0
learning: true
Notes
Keys and values are separated by :
Boolean values are true or false
Use spaces, never tabs
Task 2: Lists

Updated person.yaml

name: Raja Vardhan
role: DevOps Engineer
experience_years: 0
learning: true

tools:
  - Docker
  - Kubernetes
  - Git
  - Jenkins
  - Linux

hobbies: [learning, coding, cricket]
Two ways to write lists in YAML
Block Style
tools:
  - Docker
  - Kubernetes
  - Git
Inline Style
tools: [Docker, Kubernetes, Git]
Task 3: Nested Objects

server.yaml

server:
  name: web-server
  ip: 192.168.1.10
  port: 8080

database:
  host: localhost
  name: mydb

  credentials:
    user: admin
    password: secret123
What happens if you use tabs?

Example:

server:
	name: web-server

YAML validators usually return errors like:

found character '\t' that cannot start any token

or

syntax error: tabs are not allowed
Task 4: Multi-line Strings
Using | (Literal Style)
startup_script_literal: |
  #!/bin/bash
  echo "Starting application"
  systemctl start nginx

Output preserves line breaks:

#!/bin/bash
echo "Starting application"
systemctl start nginx
Using > (Folded Style)
startup_script_folded: >
  This server starts
  nginx and then
  launches the application.

Output becomes:

This server starts nginx and then launches the application.
When to use | vs >
Symbol	Use Case
`	`
>	Long descriptions, documentation, comments where line breaks don't matter
Complete server.yaml
server:
  name: web-server
  ip: 192.168.1.10
  port: 8080

database:
  host: localhost
  name: mydb

  credentials:
    user: admin
    password: secret123

startup_script_literal: |
  #!/bin/bash
  echo "Starting application"
  systemctl start nginx

startup_script_folded: >
  This server starts
  nginx and then
  launches the application.
Task 5: Validate YAML
Install yamllint
Ubuntu
sudo apt update
sudo apt install yamllint -y
Validate Files
yamllint person.yaml
yamllint server.yaml
Intentional Indentation Error

Broken YAML:

server:
 name: web-server
   ip: 192.168.1.10

Error:

syntax error: mapping values are not allowed here

or

wrong indentation

Fixed:

server:
  name: web-server
  ip: 192.168.1.10
Task 6: Spot the Difference
Correct
name: devops
tools:
  - docker
  - kubernetes
Broken
name: devops
tools:
- docker
  - kubernetes
What's wrong?

The second list item is indented differently from the first item.

YAML requires all items in the same list to have the same indentation level.

Correct version:

name: devops
tools:
  - docker
  - kubernetes
YAML Rules to Remember for CI/CD
Use spaces only, never tabs.
Indentation is critical.
Keys end with :.
Lists use -.
Booleans are true or false.
| preserves newlines.
> folds text into a single line.
YAML is case-sensitive.
Validate before using in GitHub Actions, Jenkins, Kubernetes, or Ansible.
Most CI/CD pipeline failures happen because of YAML indentation mistakes
