# Day 12 – Revision & Fundamentals Check

## 1. Mindset & Learning Plan Review
- Revisited my Day 01 DevOps learning plan.
- Current goals still feel correct.
- Need to improve more in shell scripting and troubleshooting.
- Planning to practice more hands-on commands daily.

---

## 2. Processes & Services Revision

### Commands Practiced


ps aux

Observation:

Displayed all running processes in the system.
systemctl status ssh

Observation:

Verified SSH service is active and running.
journalctl -u ssh

Observation:

Checked SSH service logs and login attempts.
3. File Skills Practice
File Operations Practiced
echo "DevOps Practice" >> notes.txt
Appended text into a file.
chmod 755 script.sh
Changed file permissions.
mkdir revision-practice
Created a new directory.
cp notes.txt backup.txt
Copied one file into another.
ls -l
Checked permissions and ownership.
4. Cheat Sheet Refresh
5 Commands I Would Use First During an Incident
ps aux
Check running processes.
systemctl status <service>
Verify service health.
journalctl -u <service>
Read service logs.
df -h
Check disk space.
top
Monitor CPU and memory usage.
5. User & Group Management Practice
Scenario Practiced
sudo useradd testuser
Created a new user.
id testuser
Verified user information.
sudo chown testuser:testuser sample.txt
Changed file ownership.
ls -l sample.txt
Verified ownership changes.
Mini Self-Check
1. Which 3 commands save you the most time right now, and why?
ls -l

Helps quickly check permissions and ownership.

systemctl status

Quickly verifies whether a service is running.

journalctl -u

Useful for troubleshooting service issues using logs.

2. How do you check if a service is healthy?

Commands:

systemctl status ssh
ps aux | grep ssh
journalctl -u ssh
3. How do you safely change ownership and permissions?

Example:

sudo chown ubuntu:ubuntu file.txt
chmod 644 file.txt
First verify ownership using ls -l
Then apply minimal required permissions.
4. What will you focus on improving in the next 3 days?
Shell scripting
awk and sed practice
Linux troubleshooting
Process monitoring
Writing reusable scripts
Key Takeaways
Revision helps retain Linux fundamentals.
Service monitoring commands are becoming easier to understand.
File permissions and ownership are very important in DevOps.
Need more confidence with shell scripting and automation.
