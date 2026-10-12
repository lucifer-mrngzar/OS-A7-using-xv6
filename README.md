<!--
Author: RANVEER GUPTA
Roll Number: 2401MC20
Course: Operating Systems
Assignment: 7
Platform: xv6
-->

# OS Assignment 7 — xv6 Kernel Extensions

**Submitted by:** Ranveer Gupta  
**Roll Number:** 2401MC20  
**Course:** Operating Systems  
**Assignment:** 7  
**Platform:** xv6 Operating System

## Overview

This repository contains the implementation and study of advanced operating system concepts through modifications to the xv6 teaching operating system. The assignment explores how operating systems manage concurrent execution, coordinate shared resources, identify deadlocks, and allocate CPU time among competing processes.

The work is organized into four modules, combining kernel-level changes with user-space programs to examine the behavior of these mechanisms in practice.

## Assignment Modules

### 1. Thread Creation and Shared Address Space

**Objective:** Extend xv6 to support multiple execution threads sharing the same address space.

- Introduce the `clone()` system call to create threads that execute a specified function using a user-provided stack.
- Implement `join()` to wait for thread termination and reclaim thread resources.
- Modify process-management structures and lifecycle operations to distinguish threads from independent processes.
- Develop `threadtest.c` to examine shared access to a global counter.

**Concepts:** Threads, address-space sharing, system calls, process lifecycle, and race conditions.

### 2. Semaphore-Based Synchronization

**Objective:** Coordinate concurrent execution and protect shared data against race conditions.

- Implement counting semaphores using kernel synchronization primitives and xv6's sleep/wakeup mechanism.
- Introduce `sem_init()`, `sem_wait()`, and `sem_signal()` system calls.
- Develop `synctest.c` to compare shared-counter operations with and without synchronization.
- Apply semaphore-based coordination to the bounded-buffer Producer–Consumer problem using `empty`, `full`, and `mutex` semaphores.

**Concepts:** Mutual exclusion, critical sections, blocking synchronization, race conditions, and producer–consumer coordination.

### 3. Deadlock Detection and Avoidance

**Objective:** Analyze resource-allocation states and identify conditions that can prevent processes from progressing.

- Implement a user-space resource-allocation model using `Allocation`, `Request` or `Need`, and `Available` matrices.
- Develop a deadlock detection routine to identify processes that cannot complete under the simulated resource state.
- Implement the Banker's safety algorithm to determine whether a resource-allocation state is safe.
- Explore circular-wait scenarios involving processes and pipes, where supported by the implementation.

**Concepts:** Deadlock conditions, resource allocation, safe sequences, unsafe states, and deadlock detection versus avoidance.

### 4. Priority-Based Preemptive CPU Scheduling

**Objective:** Modify the default xv6 scheduling policy to account for process priorities and reduce starvation.

- Add priority-related fields to the process control structure.
- Introduce `set_priority()` and `get_priority()` system calls.
- Select runnable processes according to their priority, with an appropriate tie-breaking policy.
- Implement aging to improve the priority of processes that remain runnable but wait too long.
- Develop `priotest.c` to examine execution order and scheduling behavior across different priorities.

**Concepts:** CPU scheduling, preemption, priority inversion considerations, waiting time, turnaround time, and starvation prevention.

## Implementation Approach

The assignment follows a kernel-extension approach:

1. **Kernel modifications:** Update process management, scheduling, synchronization, and system-call handling where required.
2. **User-space interface:** Expose the new functionality through system calls and supporting headers.
3. **Test programs:** Build dedicated programs to exercise each feature independently.
4. **Behavioral analysis:** Compare execution behavior, inspect terminal output, and evaluate the correctness of the implemented mechanisms.

## Repository Structure

The repository is organized around the following implementation components. File locations may vary depending on the xv6 version and the final project layout.

```text
OS_Assignment_7_xv6/
├── kernel/
│   ├── proc.c          # Process management and scheduling
│   ├── proc.h          # Process structure definitions
│   ├── syscall.c       # System-call dispatch
│   ├── syscall.h       # System-call identifiers
│   ├── sysproc.c       # Process-related system calls
│   └── ...
├── user/
│   ├── threadtest.c    # Thread creation and shared counter
│   ├── synctest.c      # Semaphore synchronization tests
│   ├── deadlock.c      # Resource-allocation algorithms
│   ├── priotest.c      # Priority scheduling tests
│   └── ...
└── README.md
```

*Note: Adjust this structure to reflect the actual files and directories in your xv6 source tree.*

## Testing and Evaluation

The following checks are intended to validate the implementation of each module.

| Module | Verification |
|---|---|
| Threads | Confirm that threads execute their assigned functions, share the intended memory, and terminate cleanly. |
| Semaphores | Compare counter results with and without synchronization; verify correct Producer–Consumer coordination. |
| Deadlocks | Test safe and unsafe resource states, and verify the detection logic using suitable scenarios. |
| Scheduling | Observe execution order, priority changes, and whether aging allows low-priority processes to progress. |

### Experimental Observations

Record the actual results obtained from your xv6 runs.

- **Threading:** Final shared-counter value and thread termination behavior.
- **Synchronization:** Counter values before and after semaphore protection, along with Producer–Consumer output.
- **Deadlock analysis:** Results for safe, unsafe, and deadlocked test cases.
- **CPU scheduling:** Process priorities, observed completion order, and aging behavior.

## Learning Outcomes

This assignment provides practical exposure to the internal mechanisms that support concurrent execution in an operating system. It connects theoretical concepts with kernel implementation, emphasizing the interaction between process management, synchronization, resource allocation, and scheduling.

The overall objective is to understand not only how these mechanisms are implemented, but also how incorrect synchronization, unsafe resource allocation, and scheduling policies can affect system behavior.

---
