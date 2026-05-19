1)Check running processes?
>ps aux | head : shows all running processes and system usage
>pgrep sshd : confirms that ssh process is running

2)Inspect one systemd service?
>selected service ssh:
>>systemctl status ssh : SSH service is active and enabled
>> systemctl list-units --type=service --state=running : Lists all currently running services managed by systemd.

3)Capture a small troubleshooting flow
>>Problem
Unable to connect using SSH.
Steps Taken
Checked if SSH process is running using:
>pgrep sshd

Verified service status:

>systemctl status ssh

Reviewed SSH logs:

>journalctl -u ssh
Checked system logs:

>tail -n 20 /var/log/syslog
