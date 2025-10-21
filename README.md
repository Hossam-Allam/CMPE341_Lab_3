# Linux Introduction 3 - Summary

## Overview
This document serves as a summary of **"the contents of lab 3"** , part of the *Operating Systems Lab (CMPE341-S01-2025)*.  
It covers Linux process management, job control, package management, and system services using `systemd`.

---

## Learning Outcomes
By the end of this lab, you should be able to:
- Explain the difference between **processes** and **jobs** in Linux.
- Manage **foreground** and **background** jobs.
- Inspect and control running processes.
- Install, remove, and query **packages**.
- Manage **systemd services** and view logs.

---

## Processes vs Jobs

| Aspect | Process | Job |
|--------|----------|-----|
| Managed by | Kernel | Shell (bash, zsh, etc.) |
| Identifier | PID (Process ID) | JID (%1, %2, etc.) |
| Description | Any running program | Command(s) started in the terminal |
| Scope | System-wide | Terminal session only |

> Every job is a process, but not every process is a job.

---

## Foreground & Background Processes

- **Foreground process (`fg`)**: Runs interactively, occupies the terminal.
- **Background process (`bg`)**: Runs independently; terminal remains usable.

---

## Common Process Management Commands

| Command | Description |
|----------|-------------|
| `ps` | Show running processes |
| `top` | Display real-time system process info |
| `kill` | Send signals to terminate processes |
| `bg` | Resume job in background |
| `fg` | Bring job to foreground |
| `df` | Show disk usage information |
| `nice` | Start a process with modified priority |
| `renice` | Change priority of an existing process |
| `pidof` | Display PID of a process |

---

## Detailed Process Monitoring

### `ps -l`
Shows process details including PID, PPID, priority (PRI), nice value (NI), and state (R, S, T, Z).

### `ps aux`
Displays system-wide process info with columns like `%CPU`, `%MEM`, `VSZ`, `RSS`, and `STAT`.

### `top`
Provides real-time system monitoring of CPU, memory, and process usage.

### `htop`
Interactive version of `top`.  
Install with:
```bash
sudo apt install htop
```

---

## Priority Management

- **Nice values range:** `-20` (highest priority) to `+19` (lowest priority)
- Default: `0`  
Commands:
```bash
nice -n <value> command
renice <new_value> -p <PID>
```

---

## Process Hierarchy

- **Parent process** creates **child processes** via `fork()`.
- **PPID** identifies the parent of each process.
- Process types:
  - Running
  - Sleeping
  - Stopped
  - Zombie
  - Orphan
  - Daemon

---

## Example Challenge Explanation

> If process 522 is terminated, its children (834, 835) become **orphan processes** and are adopted by `init`.

---

## System Services

- Services are background processes responding to system or network requests.
- Most services run as **daemons**.

### `systemd`
Manages startup and control of services using **units**.

#### Unit Types
| Type | Purpose |
|------|----------|
| `.service` | Manage daemons |
| `.socket` | Activate service on network activity |
| `.target` | Group of units |
| `.timer` | Schedule services via timers |

#### Unit File Locations
- `/usr/lib/systemd/system` → default unit files
- `/etc/systemd/system` → custom or modified units

### Common Commands
```bash
systemctl start <service>
systemctl stop <service>
systemctl restart <service>
systemctl status <service>
systemctl enable <service>
systemctl disable <service>
```

---

## Key Takeaways

- **Processes vs Jobs:** Kernel vs Shell concepts.
- **Process Control:** `ps`, `kill`, `nice`, `renice`.
- **System Monitoring:** `top`, `htop`.
- **System Services:** Managed by `systemd` using `systemctl`.

---

## References
GitHub Repository: [CMPE341_Lab_3](https://github.com/Operating-Systems-Lab-Linux/CMPE341_Lab_3)
