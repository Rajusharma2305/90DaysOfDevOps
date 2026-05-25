Task-1

create users in home directory:

sudo useradd -m tokyo
sudo useradd -m berlin
sudo useradd -m professor

create passwords for users:

sudo passwd tokyo
sudo passwd berlin
sudo passwd professor

verify users:

cat /etc/passwd | grep tokyo
cat /etc/passwd | grep berlin
cat /etc/passwd | grep professor


Task2:


create groups:
sudo groupadd developers
sudo groupadd admins

verify groups:
cat /etc/group | grep developers
cat /etc/group | grep admins

Task3:
Assign users to groups:

sudo usermod -aG developers tokyo

sudo usermod -aG developers,admins berlin

sudo usermod -aG admins professor

verify group membership:

groups tokyo
groups berlin
groups professor

task4:

make directory:
sudo mkdir /home/ubuntu/dev-project

change group ownership:
sudo chown :developers /home/ubuntu/dev-project

Create directory
sudo mkdir /opt/dev-project
Change group owner
sudo chown :developers /opt/dev-project
Set permissions
sudo chmod 775 /opt/dev-project
Verify permissions
ls -ld /opt/dev-project

Expected:

drwxrwxr-x
Test file creation as tokyo

Switch user:

su - tokyo

Create file:

touch /opt/dev-project/tokyo-file.txt

Exit:

exit
Test file creation as berlin

Switch user:

su - berlin

Create file:

touch /opt/dev-project/berlin-file.txt

Exit:

exit
Verify files
ls -l /opt/dev-project



Task 5: Team Workspace
Create user
sudo useradd -m nairobi
sudo passwd nairobi
Create group
sudo groupadd project-team
Add users to group
sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo
Create workspace directory
sudo mkdir /opt/team-workspace
Set group ownership
sudo chown :project-team /opt/team-workspace
Set permissions
sudo chmod 775 /opt/team-workspace
Test as nairobi

Switch user:

su - nairobi

Create file:

touch /opt/team-workspace/nairobi-file.txt

Exit:

exit
