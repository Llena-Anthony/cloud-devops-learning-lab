# Linux Process Monitoring Command Reference

| Command | Use |
| --- | --- |
| `ps aux` | View a snapshot of processes from all users with resource columns. |
| `ps aux --sort=-%cpu \| head` | Show the highest CPU consumers first. |
| `ps -p <PID> -o pid,user,%cpu,%mem,stat,etime,cmd` | Inspect a selected process by PID. |
| `pgrep -a yes` | Find active `yes` test processes and show their commands. |
| `kill <PID>` | Request a process to stop gracefully. |

Use the PID from current output, validate the command and owner, and prefer a normal `kill` before considering stronger signals. Commands are references; they were not run as part of this documentation update.
