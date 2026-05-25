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
