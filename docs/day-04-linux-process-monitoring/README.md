# Day 4: Linux Process and Resource Monitoring

## Objective

Practice inspecting Linux processes and investigating CPU consumption on an AWS EC2 Linux instance. The focus was to identify active processes, interpret process information, and use a controlled workload to observe CPU pressure safely.

## Environment

- Platform: AWS EC2
- Operating system: Linux instance accessed through the shell
- Scope: process and CPU observation only

No instance identifiers, public IP addresses, SSH keys, or credentials are recorded in this journal.

## Concepts Practiced

- Viewing the processes currently running on a Linux host
- Recognizing a process by its process ID (PID), owner, state, and command
- Comparing CPU and memory use to focus an investigation
- Distinguishing normal background services from a process that needs attention
- Using an EC2 instance as a safe environment to build Linux troubleshooting habits

Process monitoring is a point-in-time investigation: a high CPU value is a signal to investigate, not by itself proof that a process is faulty.

## `ps aux` Process Information

`ps aux` displays a broad snapshot of processes from all users. I used it to see which commands were running and who owned them.

| Field | Meaning |
| --- | --- |
| `USER` | Account that owns the process |
| `PID` | Unique process ID |
| `%CPU` / `%MEM` | CPU and memory use reported by `ps` |
| `VSZ` / `RSS` | Virtual-memory size and resident physical memory (KiB) |
| `TTY` | Controlling terminal, if any |
| `STAT` | Process state and scheduler flags |
| `START` / `TIME` | Start time and accumulated CPU time |
| `COMMAND` | Command that started the process |

## CPU Sorting and Identification

I sorted the process list by descending CPU use with:

```bash
ps aux --sort=-%cpu | head
```

This places the highest CPU consumers at the top of a short list. I then used the PID, owner, command, and CPU percentage together to identify which process was responsible. The command is useful for initial triage; a follow-up check should confirm whether the workload is expected before stopping anything.
