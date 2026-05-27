# Day 08 – Cloud Deployment with Nginx

## Goal
Deploy a real web server on a cloud VM and practice basic server management.

---

# Part 1: Launch Cloud Instance & SSH Access

## Step 1: Create Cloud Instance

### AWS EC2
- Launched Ubuntu EC2 instance
- Selected key pair
- Allowed:
  - SSH (Port 22)
  - HTTP (Port 80)

### Instance Details
- OS: Ubuntu
- Type: t2.micro

---

## Step 2: Connect via SSH

### AWS

```bash
chmod 400 my-key.pem
ssh -i my-key.pem ubuntu@<your-instance-ip>

Connection successful.

Part 2: Install Docker & Nginx
Step 1: Update System
sudo apt update
sudo apt upgrade -y
Step 2: Install Docker
sudo apt install docker.io -y

Verify Docker:

docker --version
Step 3: Install Nginx
sudo apt install nginx -y

Verify Nginx status:

systemctl status nginx

Start Nginx if needed:

sudo systemctl start nginx

Enable on boot:

sudo systemctl enable nginx
Part 3: Security Group Configuration
Allowed Inbound Rules
Type	Port
SSH	22
HTTP	80
Test Web Access

Opened browser and visited:

http://<your-instance-ip>

Successfully viewed the Nginx welcome page.

📸 Screenshot captured for submission.

Part 4: Extract Nginx Logs
Step 1: View Nginx Logs

Access logs:

cat /var/log/nginx/access.log

Error logs:

cat /var/log/nginx/error.log
Step 2: Save Logs to File
cat /var/log/nginx/access.log > ~/nginx-logs.txt

Verify:

cat ~/nginx-logs.txt
Step 3: Download Logs to Local Machine
AWS

Run on local terminal:

scp -i my-key.pem ubuntu@<your-instance-ip>:~/nginx-logs.txt .

Log file downloaded successfully.
