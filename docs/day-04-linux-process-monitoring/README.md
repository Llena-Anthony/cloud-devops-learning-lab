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
