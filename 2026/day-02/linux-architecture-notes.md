1)The core components of Linux (kernel, user space, init/systemd)
.kernal:
kernal is the core part of linux system it acts as a bridge between software and hardware
.userspace:
userspace is the space where the user runs application ex:vscode
.init/systemd:
When Linux boots, the kernel starts the first process called init.
Modern Linux systems mostly use systemd as the init system.its pid is 1

2)how process are created and managed?
A process is a running program.

Examples:

nginx
ssh
python script
Process Creation

Linux creates processes mainly using:

fork() → creates a copy of the parent process
exec() → loads a new program into the process

Example:
When you run:

ls

Steps:

Shell creates a new process using fork()
Child process runs ls using exec()
Kernel manages execution
Process Management

The kernel manages:

CPU scheduling
Memory allocation
Process priority
Process states

Common process states:

Running
Sleeping
Stopped
Zombie


3)What systemd Does and Why It Matters
systemd is a service manager and init system.

It:

Starts services automatically
Tracks service status
Restarts failed services
Manages logs with journald
why?
As a DevOps engineer, you will troubleshoot servers and applications regularly.

systemd helps you:

Monitor services
Debug failures
Automate startup
Analyze logs quickly

