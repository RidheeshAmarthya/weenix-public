This file contains quick instructions for getting Weenix to run on
Redhat-derived or Debian-derived Linux flavors.  See the documentation in doc/
for detailed instructions.

1. Download and install dependencies.

   On recent versions of Ubuntu or Debian, you can simply run:

   $ sudo apt-get install git-core build-essential gcc gdb qemu genisoimage make python python-argparse cscope xterm bash grub xorriso

   or on Redhat:

   $ sudo yum install git-core gcc gdb qemu genisoimage make python python-argparse cscope xterm bash grub2-tools xorriso

2. Compile Weenix:

   $ make

3. Invoke Weenix:

   $ ./weenix -n

   or, to run Weenix under gdb, run:

   $ ./weenix -n -d gdb


---

## Screenshots

### Compilation and Execution
![Execution Screenshot](https://imgur.com/l8yyPpb.png)


# Weenix Operating System Project  

## Overview  
The Weenix Operating System is a modular, Unix-like kernel developed as part of USC’s CSCI 420 (Operating Systems) course. This project involved building core kernel components, including process management, threading, virtual memory, and a file system, entirely from scratch in C.  

This project challenged me to design and debug intricate low-level systems while ensuring seamless integration across various subsystems, requiring a deep understanding of computer architecture and operating system principles.  

> **Note:** Due to academic policies, the actual kernel source code cannot be shared publicly. Below is a detailed breakdown of the project’s complexity and my contributions.  

---

## My Contributions  

### 1. **Process Management and Threading**  
- **Kernel Threading**:  
  - Implemented kernel-level threading with **preemptive multitasking**, including context-switching logic using assembly-level manipulation of CPU registers and stack frames.  
  - Designed a lightweight thread control block (TCB) to manage thread metadata, ensuring efficient scheduling and lifecycle management.  

- **Scheduler**:  
  - Built a priority-based **round-robin scheduler** to manage thread execution.  
  - Integrated thread states (READY, RUNNING, WAITING) and implemented logic for thread blocking on synchronization primitives like locks and condition variables.  

- **Process Hierarchies**:  
  - Developed parent-child relationships in process management, enabling functionalities like `wait()` and proper handling of orphaned processes via reparenting to `init`.  

---

### 2. **Virtual Memory (VM)**  
- **Page Tables and Demand Paging**:  
  - Designed a two-level paging mechanism, implementing virtual-to-physical address translation using page tables.  
  - Implemented **demand paging**, ensuring efficient memory usage by loading pages into physical memory only on access, leveraging page faults for lazy allocation.  

- **Copy-on-Write (CoW)**:  
  - Optimized memory allocation by implementing CoW for forked processes, ensuring that pages are shared until modified, reducing unnecessary memory duplication.  

- **Swapping Mechanism**:  
  - Integrated a basic swapping system that offloads inactive pages to disk to handle memory pressure situations effectively.  

---

### 3. **File System**  
- **VFS (Virtual File System) Layer**:  
  - Designed an abstract file system interface to unify access to different file system implementations.  
  - Implemented inode-based file access, ensuring efficient file and directory traversal.  

- **System Call Integration**:  
  - Implemented system calls for file manipulation, including `open()`, `read()`, `write()`, `close()`, and `lseek()`.  
  - Extended support for directory operations like `mkdir()`, `rmdir()`, and `readdir()`.  

- **Caching Mechanisms**:  
  - Built a block-level disk cache to minimize I/O operations and improve performance. The cache uses an **LRU eviction policy** to manage memory usage effectively.  

---

### 4. **Synchronization and Concurrency**  
- **Locks and Semaphores**:  
  - Designed low-level synchronization primitives, including spinlocks and mutexes, to manage concurrent access to shared kernel resources.  

- **Condition Variables**:  
  - Implemented condition variables for signaling between threads in scenarios like producer-consumer problems.  

- **Deadlock Prevention**:  
  - Integrated deadlock detection and resolution mechanisms for kernel-level resource management.  

---

### 5. **Debugging and Optimization**  
- Debugged complex kernel crashes and race conditions using **GDB** and custom kernel debugging tools, analyzing core dumps and stack traces.  
- Profiled system performance using custom metrics for scheduling latency, memory utilization, and I/O throughput.  

---

## Learning Outcomes  
Through this project, I gained hands-on experience with:  
- **Low-Level Systems Programming**: Mastery in C programming for kernel development, including inline assembly for context switching.  
- **Memory Management**: Designing efficient paging and swapping mechanisms while understanding performance trade-offs.  
- **Concurrency Challenges**: Debugging race conditions, deadlocks, and priority inversion in multithreaded environments.  
- **Kernel-Level I/O**: Developing file system layers and understanding I/O scheduling.  

---

## Skills Demonstrated  
- Advanced C Programming  
- Operating System Architecture: Virtual Memory, File Systems, Scheduling  
- Low-Level Debugging: GDB, custom logging tools  
- Synchronization: Spinlocks, Mutexes, Semaphores, Condition Variables  
- Performance Optimization  

---

## Disclaimer  
This repository serves as an overview of my work on the Weenix project. Actual implementation details are not shared here to comply with academic integrity policies.  

If you're interested in learning more or discussing the technical details, feel free to reach out for a private discussion at vridheesh@gmail.com

---
