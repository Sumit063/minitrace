# minitrace

A minimal, user-space system call tracer for Linux, inspired by strace, built from scratch using the ptrace system call.

This project focuses on understanding how processes interact with the Linux kernel by intercepting and observing system calls at runtime.

## Motivation
Modern applications abstract away operating system behavior, but performance issues, crashes, and security bugs often originate at the user–kernel boundary.

This project was built to:
- Understand how debuggers and tracers work internally
- Observe real system calls made by a process
- Explore Linux process control, signals, and registers
- Gain hands-on experience with low-level OS interfaces

This is a core systems / operating systems project, not a web or framework-based application.

## What minitrace does (current scope)
- Launches a target program under tracing
- Intercepts every system call entry and exit
- Prints the syscall number and return value
- Correctly handles process lifecycle events
- Runs entirely in user space

Example usage:
```bash
./minitrace /bin/ls -l
```

Example output:
```text
syscall(59) = 0
syscall(12) = 938249216
syscall(9) = 140295364730880
```

## How it works (high level)
- fork() creates a child process
- The child enables tracing with PTRACE_TRACEME
- The parent drives execution using PTRACE_SYSCALL
- CPU registers are inspected at syscall entry and exit
- Syscall metadata is extracted directly from registers

## Build
Requirements:
- Linux (tested on Ubuntu via WSL2)
- x86_64 architecture
- GCC toolchain

### Compile:
```bash
gcc -O2 -Wall -Wextra -std=c11 minitrace.c -o minitrace
```

## Run
```bash
./minitrace <command> [args...]
```

Examples:
```bash
./minitrace /bin/echo hello
./minitrace /bin/ls -l
```

## Platform notes
- Designed for Linux x86_64
- Uses Linux-specific interfaces (ptrace, /proc, CPU registers)
- Not portable to macOS or Windows without a Linux kernel
- Tested under WSL2, which provides full ptrace support

## Roadmap
- Map syscall numbers to names
- Decode arguments for common syscalls
- Add syscall filtering
- Show only failed syscalls
- Handle forked processes
- Add basic syscall latency measurement

## Learning outcomes
- Linux process lifecycle and signals
- System call ABI and kernel boundary
- User-space debugging and tracing internals
- Low-level performance analysis foundations

## License
MIT

---

Built by **[Sumit Pandey](https://sumitpandey.online)** · [GitHub](https://github.com/Sumit063) · [LinkedIn](https://www.linkedin.com/in/sumit063)
