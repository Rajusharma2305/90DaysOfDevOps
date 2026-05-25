Task 1: Create Files
Create empty file
touch devops.txt
Create notes.txt with content

Using echo:

echo "Linux permissions practice" > notes.txt

OR using cat:

cat > notes.txt

Type:

Linux permissions practice

Press:

CTRL + D
Create script.sh using vim
vim script.sh

Press i → insert mode

Add:

echo "Hello DevOps"

Save and exit:

ESC
:wq
Verify files and permissions
ls -l

Example output:

-rw-rw-r-- 1 ubuntu ubuntu   0 devops.txt
-rw-rw-r-- 1 ubuntu ubuntu  28 notes.txt
-rw-rw-r-- 1 ubuntu ubuntu  21 script.sh
Task 2: Read Files
Read notes.txt
cat notes.txt
Open script.sh in read-only mode
vim -R script.sh
First 5 lines of /etc/passwd
head -5 /etc/passwd
Last 5 lines of /etc/passwd
tail -5 /etc/passwd
Task 3: Understand Permissions

Permission format:

rwxrwxrwx

Split into:

owner | group | others

Meaning:

r = read = 4
w = write = 2
x = execute = 1
Check permissions
ls -l devops.txt notes.txt script.sh

Example:

-rw-rw-r--  devops.txt

Explanation:

Permission	Meaning
Owner: rw-	Owner can read and write
Group: rw-	Group can read and write
Others: r--	Others can only read
Task 4: Modify Permissions
Make script executable
chmod +x script.sh

Check:

ls -l script.sh

Expected:

-rwxrwxr-x

Run script:

./script.sh

Output:

Hello DevOps
Make devops.txt read-only

Remove write permission for everyone:

chmod a-w devops.txt

Verify:

ls -l devops.txt

Expected:

-r--r--r--
Set notes.txt permission to 640
chmod 640 notes.txt

Meaning:

Owner → read + write
Group → read
Others → no permission

Verify:

ls -l notes.txt

Expected:

-rw-r-----
Create project directory with 755
mkdir project

Set permissions:

chmod 755 project

Verify:

ls -ld project

Expected:

drwxr-xr-x
Task 5: Test Permissions
Try writing to read-only file
echo "test" >> devops.txt

Expected error:

Permission denied
Remove execute permission from script
chmod -x script.sh

Try running:

./script.sh

Expected error:

Permission denied
