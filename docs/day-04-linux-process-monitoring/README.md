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

## Controlled CPU Load Experiment

To create a short-lived, intentional CPU workload, I started `yes` processes in separate shell sessions and watched the sorted `ps` output:

```bash
yes > /dev/null
```

Each `yes` process continuously writes output that is discarded, making it suitable only for controlled testing. During the exercise, multiple `yes` processes appeared near the top of the CPU-sorted list at approximately 100% CPU each. I treated this as an expected result of the test and ended the test processes after observation. No terminal output is reproduced here.

> Caution: Run synthetic load only on an instance you control, for a short time, and account for EC2 capacity and cost.

## Troubleshooting Observations

- CPU sorting quickly made the intentionally created `yes` workload visible.
- Multiple high-CPU processes can be legitimate when they match an expected test or workload.
- PID alone is not enough context; checking `USER` and `COMMAND` reduces the chance of stopping the wrong process.
- A process snapshot changes quickly, so repeat the command when investigating an active issue.

## Lessons Learned

Start with a broad process view, sort it by the resource under pressure, verify the process context, then take the least disruptive action. This is more reliable than terminating a process solely because it is at the top of a list.
