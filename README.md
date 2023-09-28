- [1. Why Operating Systems (2023-09-07)](#1-why-operating-systems-2023-09-07)
  - [1.1. Core Operating Systems Concepts:](#11-core-operating-systems-concepts)
  - [1.2. Code example](#12-code-example)
- [2. Kernels (2023-09-18)](#2-kernels-2023-09-18)
  - [2.1. Instruction Set Architecture (ISA)](#21-instruction-set-architecture-isa)
  - [2.2. Inter-Process Communication (IPC)](#22-inter-process-communication-ipc)
  - [2.3. Intro to System calls](#23-intro-to-system-calls)
    - [2.3.1. `write()`](#231-write)
    - [2.3.2. `exit_group()`](#232-exit_group)
    - [2.3.3. Standard File Descriptors](#233-standard-file-descriptors)
  - [2.4. API vs. ABI](#24-api-vs-abi)
    - [2.4.1. ABI Details to Execute OS "Functions"/System Calls](#241-abi-details-to-execute-os-functionssystem-calls)
    - [2.4.2. ELF File Format](#242-elf-file-format)
    - [2.4.3. How ELF Files Are Structured](#243-how-elf-files-are-structured)
  - [2.5. Kernel vs. User Mode](#25-kernel-vs-user-mode)
    - [2.5.1. System Calls](#251-system-calls)
    - [2.5.2. `strace`](#252-strace)
    - [2.5.3. Kernel as a Long Running Program](#253-kernel-as-a-long-running-program)
    - [2.5.4. Types of Kernels](#254-types-of-kernels)
  - [2.6. PRACTICE](#26-practice)
- [3. Libraries (2023-09-13)](#3-libraries-2023-09-13)
  - [3.1. Applications Use Libraries](#31-applications-use-libraries)
  - [3.2. How Libraries Are Used To Compile C Code](#32-how-libraries-are-used-to-compile-c-code)
    - [3.2.1. Compilation in C](#321-compilation-in-c)
    - [3.2.2. Static Libraries](#322-static-libraries)
      - [3.2.2.1. Static libraries included at LINK time](#3221-static-libraries-included-at-link-time)
    - [3.2.3. Dynamic Libraries](#323-dynamic-libraries)
      - [3.2.3.1. Dynamic libraries included at RUN time](#3231-dynamic-libraries-included-at-run-time)
      - [3.2.3.2. `>>> ldd <EXE>`](#3232--ldd-exe)
  - [3.3. Static vs. Dynamic Libraries](#33-static-vs-dynamic-libraries)
    - [3.3.1. HOW Dynamic Libraries Can Break Executables](#331-how-dynamic-libraries-can-break-executables)
      - [3.3.1.1. Dynamic Libraries \& Memory Leaks](#3311-dynamic-libraries--memory-leaks)
    - [3.3.2. How Semantic Versioning Reflects Dynamic Library Changes](#332-how-semantic-versioning-reflects-dynamic-library-changes)
  - [3.4. System Calls vs. C Standard Library Functions](#34-system-calls-vs-c-standard-library-functions)
    - [3.4.1. C `atexit` (vs. System call `exit()` / `exit_group()`)](#341-c-atexit-vs-system-call-exit--exit_group)
  - [3.5. PRACTICE:](#35-practice)
- [4. Process Creation (2023-09-15)](#4-process-creation-2023-09-15)
  - [4.1. Process Control Blocks (PCBs)](#41-process-control-blocks-pcbs)
  - [4.2. Process State Diagrams](#42-process-state-diagrams)
  - [4.3. Reading Process States via `/proc`](#43-reading-process-states-via-proc)
  - [4.4. Creating New Processes (via Cloning)](#44-creating-new-processes-via-cloning)
    - [4.4.1. `fork()`](#441-fork)
      - [4.4.1.1. `getpid()` \& `getppid()`](#4411-getpid--getppid)
      - [4.4.1.2. `fork()` Example](#4412-fork-example)
  - [4.5. PRACTICE](#45-practice)
- [5. Process Management (2023-09-16)](#5-process-management-2023-09-16)
  - [5.1. `execve()`](#51-execve)
    - [5.1.1. `execve()` Example](#511-execve-example)
  - [5.2. Process States](#52-process-states)
    - [5.2.1. Process/Kernel Startup via `init`](#521-processkernel-startup-via-init)
    - [5.2.2. Process Tree (Parent/Child Graph) Example](#522-process-tree-parentchild-graph-example)
    - [5.2.3. pid Logistics](#523-pid-logistics)
    - [5.2.4. Process Address Space](#524-process-address-space)
  - [5.3. Parent/Child `exit()`-ing](#53-parentchild-exit-ing)
    - [5.3.1. Calling `wait()` on Child Processes](#531-calling-wait-on-child-processes)
      - [5.3.1.1. `wait()` Example](#5311-wait-example)
    - [5.3.2. Zombie Process](#532-zombie-process)
      - [5.3.2.1. Zombie Example](#5321-zombie-example)
    - [5.3.3. Orphan Process](#533-orphan-process)
      - [5.3.3.1. Orphan Example](#5331-orphan-example)
  - [5.4. PRACTICE](#54-practice)
- [6. Basic IPC (2023-09-19)](#6-basic-ipc-2023-09-19)
  - [6.1. Reading/Writing to Files/Standard-(In/Out)](#61-readingwriting-to-filesstandard-inout)
    - [6.1.1. `cat` Terminal Example (echo input)](#611-cat-terminal-example-echo-input)
    - [6.1.2. `cat` File Example (read file)](#612-cat-file-example-read-file)
  - [6.2. Redirecting Standard File Descriptors Using The Shell (`<`, `>`, `|`)](#62-redirecting-standard-file-descriptors-using-the-shell---)
  - [6.3. Signals](#63-signals)
    - [6.3.1. `sigaction()`](#631-sigaction)
      - [6.3.1.1. Common Signal Numbers (in Linux)](#6311-common-signal-numbers-in-linux)
    - [6.3.2. How Signal Handlers Work](#632-how-signal-handlers-work)
      - [6.3.2.1. `sigaction()` Example 1](#6321-sigaction-example-1)
      - [6.3.2.2. `sigaction()` Example 2 (`read()` Error Handling)](#6322-sigaction-example-2-read-error-handling)
    - [6.3.3. Sending Signals via `kill` in the Terminal](#633-sending-signals-via-kill-in-the-terminal)
    - [6.3.4. `pidof`](#634-pidof)
  - [6.4. Non-blocking Calls](#64-non-blocking-calls)
    - [6.4.1. Blocking vs. Non-blocking Calls](#641-blocking-vs-non-blocking-calls)
    - [6.4.2. `waitpid()` vs. `wait()`](#642-waitpid-vs-wait)
    - [6.4.3. Polling](#643-polling)
    - [6.4.4. Using Interrupt Handlers](#644-using-interrupt-handlers)
      - [6.4.4.1. Interrupt Handlers Run to Completion](#6441-interrupt-handlers-run-to-completion)
      - [6.4.4.2. 3 Terms for "Interrupts" on RISC-V CPUs](#6442-3-terms-for-interrupts-on-risc-v-cpus)
  - [6.5. PRACTICE](#65-practice)
- [7. Process Practice (2023-09-21)](#7-process-practice-2023-09-21)
  - [7.1. Multiprogramming](#71-multiprogramming)
    - [7.1.1. Scheduler](#711-scheduler)
    - [7.1.2. How Switching/Swapping Processes Works (via Core Scheduling Loop)](#712-how-switchingswapping-processes-works-via-core-scheduling-loop)
    - [7.1.3. COOPERATIVE vs. TRUE Multitasking](#713-cooperative-vs-true-multitasking)
    - [7.1.4. Context Switching = Swapping Processes](#714-context-switching--swapping-processes)
  - [7.2. `pipe()`](#72-pipe)
    - [7.2.1. `pipe()` Example](#721-pipe-example)
  - [7.3. Using `&` in Shell](#73-using--in-shell)
  - [7.4. PRACTICE](#74-practice)
    - [7.4.1. 2022 Final Q2](#741-2022-final-q2)
- [8. Subprocess (2023-09-22)](#8-subprocess-2023-09-22)
  - [8.1. Lab 2 Goals](#81-lab-2-goals)
  - [8.2. Easier to Use C APIs](#82-easier-to-use-c-apis)
    - [8.2.1. `execlp()`](#821-execlp)
    - [8.2.2. `dup()` \& `dup2()`](#822-dup--dup2)
  - [8.3. Subprocess Example](#83-subprocess-example)
    - [8.3.1. Skeleton](#831-skeleton)
    - [8.3.2. Tasks To Do](#832-tasks-to-do)
    - [8.3.3. Completed Code](#833-completed-code)
      - [8.3.3.1. Visualization of Pipes](#8331-visualization-of-pipes)


<!--------------------------------{.gray}------------------------------>






<hr style="border:30px solid #FFFF; margin: 100px 0 100px 0; {.gray}"> </hr>






<!--------------------------------{.gray}------------------------------>

<div style="page-break-after: always;"></div>

# 1. Why Operating Systems (2023-09-07)

Pre-requisites:
- C programming and debugging
- Converting between bianry, hex, decimal
- Little-endian, big-endian
- Byte-addressable memory, memory address ala pointers

---

## 1.1. Core Operating Systems Concepts:
1. Virtualization -- share one resource by mimicking multiple independent copies
2. Concurrency -- handle multiple things happening at the same time
3. Persistence -- retain data consistency even w/o power

---


OS Abstractions:
- Program -- a file containing all instructions & data required to run
- Process -- an instance of running a program

---

Basic Requiremnts For A Process:
- Virtual Memory/Registers
  - Stack
  - Heap
    - process assumes it has access to all physical memory in the computer; actual memory management done by os
    - registers are independent from each other

> ---

***Q:*** the compiler needs to pick an address for each variable when compiling; what issues would be present with a global registry of addresses? {.lr}

***A:*** unsafe memory allocation/deletion ala programs read/writing each other's memory. {.lg}

> ---

## 1.2. Code example


All example code from lectures is available at https://laforge.eecg.utoronto.ca/ece344/2023-fall/student/materials.

Code compilation example:
```cpp
cd lectures/01-why-operating-systems
meson setup build
meson compile -C build

// execute code
build/read-four-bytes <FILE>
```
Source: https://laforge.eecg.utoronto.ca/ece344/2023-fall/student/materials/-/blob/main/lectures/01-why-operating-systems/read-four-bytes.c?ref_type=heads














# 2. Kernels (2023-09-18)

## 2.1. Instruction Set Architecture (ISA)
Refers to machine code that a CPU understands.

3 main ISAs in use today:
- `x86-64 / amd64` - desktops
- `aarch64 / arm64` - mobile
- `riscv / rv64gc` - open source ARM alternative

## 2.2. Inter-Process Communication (IPC)
- **IPC** -- mechanism that allows OS to transfer data between processes

- **File Descriptor** -- **not just a file**; a resource that users can either read bytes from or write bytes to; is identified by an index stored in a process
  - e.g. .txt file, ANY file, **terminal**

## 2.3. Intro to System calls

System calls are C functions that operate on/using the OS; [system calls](#system-calls) are the interface between [user & kernel mode](#kernel-mode-user-mode).

### 2.3.1. `write()`
```c
/**
 * Writes bytes from a buffer to a file descriptor.
 *
 * @param: fd - The file descriptor to write to.
 * @param: buf - A pointer to the start of the buffer.
 * @param: count - The number of bytes to write from the buffer.
 *
 * @return: The number of bytes written, or -1 on error.
 */
ssize_t write(int fd, const void *buf, size_t count);
```

### 2.3.2. `exit_group()`
Exits the current process & sets an exit status code (0 status code = no errors; is why `main()` has `return 0`).
```c
/**
 * Terminates all threads in a process and exits with the specified status code.
 *
 * @param: status - The exit status code (0-255).
 * @return: This function does not return.
 */
void exit_group(int status);
```

### 2.3.3. Standard File Descriptors
- `0` (`stdin`) -- standard input (read)
- `1` (`stdout`) -- standard output (write)
- `2` (`stderr`) -- standard error (**write**{.b})

## 2.4. API vs. ABI
- API (Application PROGRAMMING Interface) -- abstracts process details, only describes arguments & return value of a function
- ABI (Application **BINARY** Interface) -- **specifies details**, including how to pass arguments (e.g. on stack) & where the return value is

### 2.4.1. ABI Details to Execute OS "Functions"/System Calls
OS "functions" (i.e. system call) do not have addresses; instead, to run a system call for the OS we need to generate an interrupt with a `svc` instruction **using registers for arguments** (instead of stack).
```c
// e.g.

// x8 - system call number
// x0 - 1st argument
// x1 - 2nd argument
// x2 - ...
```

### 2.4.2. ELF File Format
ELF (Executable & Linkable Format):
- Present in both executables & libraries
- Always starts with either:
  - 4 bytes: `0x7F 0x45 0x4C 0x46`, or
  - ASCII encoding: `DEL 'E' 'L' 'F'`

### 2.4.3. How ELF Files Are Structured
1. **File header** -- endianness, ISA, ABI, entry point
2. **Program header** -- what to load into memory & where
3. **Instructions**
4. **Data**

## 2.5. Kernel vs. User Mode

- **Kernel Mode** -- CPU privilege level that gives access to more instructions; limits what software can interact with hardware (e.g. only kernel can manage virtual memory for processes)


| **CPU MODE**         | **SOFTWARE**            | **PRIVILEGE LEVEL** |
| -------------------- | ----------------------- | ------------------- |
| U-mode (User)        | Applications, libraries | *Least privileged*  |
| S-mode (Supervisor) | Kernel                  | ↓                   |
| H-mode (Hypervisor)  | Virtual Machines        | ↓                   |
| M-mode (Machines)    | Bootloader, firmware    | *Most privileged*   |

### 2.5.1. System Calls

***Q:*** how do we execute software in kernel mode? {.lr}

***A:*** using system calls -- allow us to perform operations in kernel space by executing code in user space; is the only **interface between user space & kernel space in Linux**:
```bash
read write open close stat mmap brk pipe clone fork
execve exit wait4 chdir  mkdir rmdir creat mount
init_module delete_module clock_nanosleep exit_group
```

### 2.5.2. `strace`
Allows us to trace (i.e. see) all system calls a Linux process makes.
```c
// e.g. running strace on Hello world assembly program

// >>> strace ./hello-world-linux-aarch64
execve("./hello_world", ["./hello_world"], 0x7ffd0489de40 /* 46 vars */) = 0
write(1, "Hello world\n", 12)           = 12
exit_group(0)                           = ?
+++ exited with 0 +++
```
- Running `strace` on JS & Python processes shows more lines than C processes because those languages are less efficient & compile to larger files.

### 2.5.3. Kernel as a Long Running Program
- Kernel has no `main()`; instead, code (termed **modules**) is executed on-demand (e.g. new hardware, specific file access, manual loading)
- Kernel modules can execute privileged instructions & access kernel data (i.e. that might be inaccessible via [system calls](#system-calls))

### 2.5.4. Types of Kernels
- **Monolithic** -- runs **all** OS services in kernel mode; kernel codebase is large
- **Microkernel** -- runs **minimum amount** of OS services in kernel mode (minimizes security risk)
- **Hybrid** -- e.g. emulation service to user mode (Windows), device driver to user mode (macOS)

## 2.6. PRACTICE

> ---

***Q:*** what does the following function do? {.r}
```c
void _start(void) {
  write(1, "Hello world\n", 12);
  exit_group(0);
}
```
***A:*** following line-by-line using the function characteristics of [`write()`](#write) & [`exit_group()`](#exit_group) ... {.lg}
* `write(1, ..., ...)`
  * Write bytes to standard output file (file descriptor = 1)
* `write(..., "Hello world\n", ...)`
  * Buffer = address of start of byte array; a string in C is an array of characters & passed as the address to the first character, so this is valid
* `write(..., ..., 12)`
  * Number of bytes to write is 12
* `exit_group(0)`
  * Exit process with no errors (status code = 0)

> ---

***Q:*** what is the difference between strings in C and in the OS (e.g. in ELF files)? {.r}

***A:*** C convention requires null-ended (`\0`) strings; ELF strings have no restrictions. {.lg}

> ---




<!--------------------------------{.gray}------------------------------>







<hr style="border:30px solid #FFFF; margin: 100px 0 100px 0; {.gray}"> </hr>






<!--------------------------------{.gray}------------------------------>
<div style="page-break-after: always;"></div>

# 3. Libraries (2023-09-13)
## 3.1. Applications Use Libraries
Applications may pass through multiple layers of libraries to function (e.g. GUI toolkit --> system daemon --> `libc`)
- an OS consists of a kernel + libraries (required for application)
  - e.g. Android & Debian both use the Linux kernel but have different applications (which necessitate different libraries, unless only simple terminal applications are used)
  - "Linux" distributions can be considered GNU/Linux because GNU distributes `libc` (standard C library) & common utilities

## 3.2. How Libraries Are Used To Compile C Code
### 3.2.1. Compilation in C
```mermaid
graph LR
	1["main.c"] --> |"Compilation"| 2("main.o*")
	2 --> |"Linkage"| 3["executable"]

	4["util.c"] --> 5["util.o"]
	5 --> 3

	6["foo.c"] --> 7["foo.o"]
	7 --> 3

	8["bar.c"] --> 9["bar.o"]
	9 --> 3
```
\*Object (`.o`) files are just [ELF files](#242-elf-file-format) with code for functions!

### 3.2.2. Static Libraries
Static libraries are what our custom C code can be compiled/archived to such that code can be repeatedly linked to an executable w/o requiring recompilation:

#### 3.2.2.1. Static libraries included at LINK time
```mermaid
graph LR
	1["util.o"] ---> |"Archive"| 2("lib.a")
	4["foo.o"] --> 2
	5["bar.o"] --> 2

  6["main.o"] --> |"Linkage"| 7("executable")
	2 ---> |"Linkage"| 7
```

### 3.2.3. Dynamic Libraries
Are for reusable code, accessed via `.so` files; can be used by multiple applications by existing in a single memory location that's accessible to applications.
- e.g. `libc.so` (C standard library) is a dynamic library

```mermaid
graph TB
	1("libc.so") --> 2["Application 1"]
	1 --> 3["Application 2"]
  1 -.-> 4["..."]
```

#### 3.2.3.1. Dynamic libraries included at RUN time

```mermaid
graph LR
	1["util.o"] ===> |"SHARED LINKAGE"| 2("lib.so")
	4["foo.o"] ==> 2
	5["bar.o"] ==> 2

  6["main.o"] --> |"Linkage"| 7("executable")
	2 -..-> |"LINKED AT RUNTIME"| 7
```

#### 3.2.3.2. `>>> ldd <EXE>`
Shows which dynamic libraries an executable uses.

## 3.3. Static vs. Dynamic Libraries

| Static Library {.p}                                               | Dynamic Library {.b}                                        |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| Prevents reusing libraries (result in many duplicates) {.lr} | Library changes/bugs can break applications {.lr}      |
| Updates to static library requires recompilation {.lr}       | Dynamic libraries can allow for easier debugging {.lg} |

### 3.3.1. HOW Dynamic Libraries Can Break Executables
Dynamic library `struct`s are laid out in memory with fields mathching the declaration order (see code below); changes in the order of lines can result in changes to the return values of ABI functions (e.g. `get_x(struct ...)`, `get_y(struct ...)` as below).

_e.g._
1. consider a dynamic library with a `struct` with multiple fields corresponding to a specific data layout (e.g. C ABI); these fields are accessible by executables
2. If a dynamic library reorders the `struct`'s fields, any executables previously using the library is using the old offsets & is now wrong

```c
// v1
struct point {
  int x; // compiler ==> x->array[0]
  int y; // compiler ==> y->array[1]
}

// v2
struct point {
  int y; // compiler ==> x->array[1] | SWITCHED!
  int x; // compiler ==> y->array[0] | SWITCHED!
}
```

#### 3.3.1.1. Dynamic Libraries & Memory Leaks
Can be investigated using Valgrind & sanitizer tools built into Clang/gcc
- Sanitizers require recompilation via the `-Db_sanitize=address` flag to Meson
  ```bash
  >>> rm -rf build
  >>> meson setup build -Db_sanitize=address
  >>> meson compile -C build
  ```

***Q:*** why would dynamic libraries specifically experience memory bugs? {.lr}

> ***A:*** "The GNU C library, which is used by all programs,
  may allocate memory for its own uses. Usually it doesn't bother to free
  that memory when the program ends—there would be no point, since the Linux
  kernel reclaims all process resources when a process exits anyway, so it
  would just slow things down." {.lg}

### 3.3.2. How Semantic Versioning Reflects Dynamic Library Changes
Given version number `MAJOR.MINOR.PATCH`, increment the:
- MAJOR version when you make incompatible API/ABI changes
- MINOR version when you add functionality in a backwards-compatible manner
- PATCH version when you make backwards-compatible bug fixes

## 3.4. System Calls vs. C Standard Library Functions
Most system calls have corresponding function calls in C, but may:
- set `errno` (explains any error that might happen with the system call if not completed succesfully)
- Buffer reads & writes (i.e. reduce # of system calls; e.g. `printf()` is buffered until its last instance, at which point many `printf()`s may be written to terminal)
- Simplify ABI (e.g. combine 2 system calls)
- Add new features
- (i.e. are not one-to-one)

### 3.4.1. C `atexit` (vs. System call `exit()` / `exit_group()`)
C `atexit(...)` calls the function in its given arguments `(...)` on program exit.

## 3.5. PRACTICE:

***Q:*** why should `printf()` be in a dynamic library? {.lr}

> ***A:*** since it is used by multiple applications, it is more efficient to have one shared copy (dynamic library) instead of a separate library for each program (static library) {.lg}






<!--------------------------------{.gray}------------------------------>







<hr style="border:30px solid #FFFF; margin: 100px 0 100px 0; {.gray}"> </hr>






<!--------------------------------{.gray}------------------------------>
<div style="page-break-after: always;"></div>

# 4. Process Creation (2023-09-15)
Recall: a process is an instance of a running program

| **// PROCESS \\\\** {.b}                    |
| -------------------------- |
| / VIRTUAL REGISTERS (MEMORY) \ {.p} |
| -- Stack {.g}                      |
| -- Heap {.g}|

## 4.1. Process Control Blocks (PCBs)

**PCB** -- keeps track of info regarding processes, including:
- Process state
- CPU registers
- Scheduling information
- Memory management information
- I/O status information
- Any other type of accounting information

## 4.2. Process State Diagrams

```mermaid
flowchart
	1(["CREATED"]) --> 2(["waiting"])
	2 <--> 3(["running"])
	3 --> 4(["blocked"])
	4 --> 2
	3 --> 5(["TERMINATED"])

```

## 4.3. Reading Process States via `/proc`
`/proc` directory contains files representing kernel's state
- subdirectories that represent processes are named with a number (process id/pid)
- state of a process is represented within `/proc/<pid>/status` (inc. name, ppid, etc.)

## 4.4. Creating New Processes (via Cloning)
it is more efficient for the os to clone a currently running process than to create a new one.

this is done by pausing the currently running process & copying its [PCB](#process-control-blocks-pcbs) into a new child process.
- Cloning copies all information from the parent (e.g. variables; note that child variables are separate from the parent's); value of information can change starting during/after [`fork()`](#441-fork)

### 4.4.1. `fork()`
`int fork(void)` clones the current process in which it is run & returns a pid in **EACH PROCESS** (parent **AND** child):
- **`0` -- in child process**
- **`>0` -- in parent process**
  - `-1` -- on failure

#### 4.4.1.1. `getpid()` & `getppid()`
- `getpid()` -- returns pid of the current process
- `getppid()` -- returns pid of the current process's parent

#### 4.4.1.2. `fork()` Example
```c
int main(void) {

  pid_t returned_pid = fork();
  /* both parent & child have variable `returned_pid`,
     but with different values */

  if (retured_pid == -1) {
    int err = errno;
    perror("fork failed");
    return err;
  }

  if (returned_pid == 0) {
    printf("Child returned pid: %d\n", returned_pid);
    printf("Child pid: %d\n", getpid());
    printf("Child parent pid: %d\n", getppid());

  } else {
    printf("Parent returned pid: %d\n", returned_pid);
    printf("Parent pid: %d\n", getpid());
    printf("Parent parent pid: %d\n", getppid());
  }

  return 0;
}
```
```console
Parent returned pid: 2341
Parent pid: 2340
Parent parent pid: 1600
Child returned pid: 0
Child pid: 2341
Child parent pid: 2340
```

## 4.5. PRACTICE


***Q:*** does parent always print before child in the [code example above](#4412-fork-example)? {.lr}

> ***A:*** no; the kernel decides when to run the parent or child process (e.g. could also run in parallel if with multiple cores, again depending on the kernel; i.e. is *non-deterministic*). {.lg}

---

***Q:*** are variables declared after a `fork()` only created in the parent process? {.lr}

> ***A:*** no; since the process is a duplicate, both the parent & child will run the same code before & after `fork()`-ing (including variable declarations after `fork()`). {.lg}
> - to have code specific to the parent or child process, we need to use conditional logic using either the [return value of `fork()`](#441-fork) or using [`getpid()`/`getppid()`](#4411-getpid--getppid).

---

***Q:*** if i `malloc()` before a `fork()`, how do we `free()` the allocated memory? {.lr}

> ***A:*** `malloc()`-ed memory can either be freed at the very end of the process OR in each conditional logic block for the parent & child process. {.lg}

---

***Q:*** given the code in the `fork()` example, how could we modify it to create a fork bomb? {.lr}

> ***A:*** calling `fork()` again in either the parent or child conditional code block will cause `fork()` to be called recursively infinitely. {.lg}






<!--------------------------------{.gray}------------------------------>







<hr style="border:30px solid #FFFF; margin: 100px 0 100px 0; {.gray}"> </hr>






<!--------------------------------{.gray}------------------------------>
<div style="page-break-after: always;"></div>

# 5. Process Management (2023-09-16)
## 5.1. `execve()`
Replaces the current process with a process indicated by a given filepath:
- `pathname`: Full path of the program to load
- `argv`: Array of strings (array of characters), terminated by a null pointer
  - Represents arguments to the process
- `envp`: Same as `argv`
  - Represents the environment of the process
- Returns an error on failure, does not return if successful

### 5.1.1. `execve()` Example

```c
int main(int argc, char *argv[]) {
  printf("This process going to become another process\n");

  // `execve()` arguments; replace current process with `ls`
  char *exec_argv[] = {"ls", NULL};
  char *exec_envp[] = {NULL};

  int exec_return = execve("/usr/bin/ls", exec_argv, exec_envp);

  if (exec_return == -1) {
    exec_return = errno;
    perror("execve failed");
    return exec_return;
  }

  printf("If execve worked, this will never print\n");
  return 0;
}
```

***Q:*** why is the item at index 0 of the `argv` array argument to `execve()` the same name as the process/executable? {.lr}

> ***A:*** because the item at index 0 is used as the executable name in many programs (e.g. you can call `ls` something else after providing `char *exec_argv[] = {"SOMETHING ELSE", "--help", NULL};`) {.lg}

## 5.2. Process States
Recall that you can look at a process' state by reading the state value from `/proc/<PID>/status` (e.g. via `/proc/<PID>/status| grep State`).

Linux processes can have 1 of 5 possible states:
- R: Running\* and runnable [Running and Waiting]
- S: Interruptible sleep [Blocked]
- D: Uninterruptible sleep [Blocked]
- T: Stopped
- Z: Zombie

\*running processes can be explicitly stopped & resumed by other processes

### 5.2.1. Process/Kernel Startup via `init`
After the kernel starts running/initializes, it creates a single process called `init` via `/sbin/init`, which:
- Is responsible for executing every other process on the machine
- Must always be active (if it exists, kernel shuts down)
- Is `systemd` in Linux

### 5.2.2. Process Tree (Parent/Child Graph) Example
Can be viewed via `htop`

```mermaid
graph TD;
  A[1: init] --> B[187: journald];
  A --> C[536: systemd --user];
  C --> D[597: gnome-shell];
  D --> E[946: firefox];
  E --> F[996: firefox tab 1];
  E --> G[1089: firefox tab 2];
  E --> H[1147: firefox tab 3];
  C --> I[1071: gnome-terminal-server];
  I --> J[1086: zsh];
  J --> K[1240: htop];
  A --> L[200: udevd];
```

### 5.2.3. pid Logistics
pids are unique for every **active** process (i.e. pids are reused after a process dies)
- pid max value is 32768
- pid value 0 is reserved (invalid)

### 5.2.4. Process Address Space
Each process has an independent view of memory (i.e. virtual memory that maps to physical memory by the kernel).

## 5.3. Parent/Child `exit()`-ing
The OS sets the exit status when a process terminates by calling `exit()`.

A parent needs to read a child process' exit status before the child process can fully exit.
- This exit status **must** be acknowledged for a child process to fully exit (otherwise waste of resources since process exists but doesn't execute anything after termination).

There are 2 possibilities for the order of exits:
- child exists first ([**zombie** process](#532-zombie-process))
- parent exists first ([**orphan** process](#533-orphan-process))

### 5.3.1. Calling `wait()` on Child Processes
To allow the parent process to read the child's exit code, we use `wait()`:
- `status` argument: address to store wait status of child process
- returns: pid of child process (with a change\*), or...
  - -1: on failure
  - 0: for non-blocking calls with no child changes\*

\**non-blocking, meaning that it returns immediately instead of waiting for a child process to exit or change state. If there are no child processes that have exited or changed state, wait returns 0 to indicate that there was no change.*

#### 5.3.1.1. `wait()` Example
Here the code **blocks** until the child process exits.
```c
int main(void) {
  // create child process
  pid_t pid = fork();
  if (pid == -1) {
    return errno;
  }

  // do nothing in parent
  if (pid == 0) {
    sleep(2);

  // call `wait` in child to exit process
  }  else {
    printf("Calling wait\n");
    int wstatus;

    // store return value of `wait` in `int wstatus`
    // if no failure, `wait` will return child pid
    pid_t wait_pid = wait(&wstatus);

    // do something on successful child process exit via `wait`
    if (WIFEXITED(wstatus)) {
      // `wait_pid` is return value of `wait()`; child pid since it was successful
      // `WEXITSTATUS(wstatus)` is 0 to indicate non-blocking
      printf("Wait returned for an exited process! pid: %d, status: %d\n", wait_pid, WEXITSTATUS(wstatus));
    }
    else {
      return ECHILD;
    }
  }

  return 0;
}
```

### 5.3.2. Zombie Process
If a process is terminated but hasn't been acknowledged (i.e. had exit status read) by a parent (e.g. due to a bug where child exit process is never read), the OS can *softly interrupt* the parent process via an ignore-able signal (a type [IPC](#22-inter-process-communication-ipc)).

- If parent ignores child termination as above, zombie process can be re-parented
- OS must keep zombie processes until ackowledgement (**meaning [PCB](#41-process-control-blocks-pcbs) of child process remains until acknowledgement**)

#### 5.3.2.1. Zombie Example
```c
int main(void) {
  // fork...

  if (pid == 0) {
    sleep(5);

  } else {
    sleep(1);
    printf("Child process state: %s", print_state(pid));

    sleep(10);
    printf("Child process state: %s", print_state(pid));
  }

  // ...
}
```
```
Child process state: S (sleeping)
Child process state: Z (zombie)
```

### 5.3.3. Orphan Process
If a parent exits before a child process, the OS re-parents the child process to `init` so that the child's exit can be acknowledged by a process.

#### 5.3.3.1. Orphan Example
```c
int main(void) {
  // fork...

  if (pid == 0) {
    // parent process still running
    printf("Child parent pid: %d\n", getppid());
    sleep(5);

    // child re-parented to `init`
    // bc parent has exited by now
    printf("Child parent pid (after sleep): %d\n", getppid());

  } else {
    // parent exits before child
    // bc parent sleeps for less time than child
    sleep(1);
  }

  // ...
}
```
```console
Child parent pid: 58061
Child parent pid (after sleep): 1
```

## 5.4. PRACTICE

***Q:*** how can zombie (child) processes be acknowledged? {.lr}

> ***A:*** after the zombie's parent dies, the zombie becomes an orphan process & gets re-parented to `init` which can then acknowledge & fully exit it. {.lg}

---

***Q:*** if the parent of a parent process (i.e. grandparent process) terminates, do the child processes become orphans? {.lr}

> ***A:*** no; parent-child process relationship is independent so the parent's parent or the child's child has no impact on whether the child to the parent becomes a zombie or orphan process. {.lg}








<!--------------------------------{.gray}------------------------------>







<hr style="border:30px solid #FFFF; margin: 100px 0 100px 0; {.gray}"> </hr>






<!--------------------------------{.gray}------------------------------>
<div style="page-break-after: always;"></div>

# 6. Basic IPC (2023-09-19)
## 6.1. Reading/Writing to Files/Standard-(In/Out)
### 6.1.1. `cat` Terminal Example (echo input)
We `read()` from standard input (fd 0) & `write()` to standard output (fd 1):
- Note: `write()` returns the number of bytes written (not always succesful!)
```c
int main() {
  char buffer[4096];
  ssize_t bytes_read;

  // `read(0, ...)` reads from STANDARD IN
  while ((bytes_read = read(0, buffer, sizeof(buffer))) > 0) {
    // `write(1, ...)` writes to STANDARD OUT (i.e. terminal)
    ssize_t bytes_written = write(1, buffer, bytes_read);

    // error handling...

    if (bytes_written == -1) {
      int err = errno;
      perror("write");
      return err;
    }
    assert(bytes_read == bytes_written);
  }

  if (bytes_read == -1) {
    int err = errno;
    perror("read");
    return err;
  }

  assert(bytes_read == 0);
  return 0;
}
```

### 6.1.2. `cat` File Example (read file)
Linux uses the lowest available file descriptor for new files, so we can close standard input (freeing file descriptor 0 as below) to open a file instead:
```c
int main(int argc, char *argv[]) {
  if (argc > 2) {
    return EINVAL;
  }

  if (argc == 2) {
    // `close` STANDARD IN file descriptor
    close(0);
    // `open` sets file descriptor 0 to given file
    int fd = open(argv[1], O_RDONLY);
    if (fd == -1) {
      int err = errno;
      perror("open");
      return err;
    }
  }

  // ...same code as 6.1.1. `cat` Example...

}
```

## 6.2. Redirecting Standard File Descriptors Using The Shell (`<`, `>`, `|`)
Replacing standard input:
```console
>>> ./program-or-file-input < program-or-file-for-output.c
```
Redirecting across multiple processes:
- 2 processes:
  ```console
  >>> cat input-file.c | ./program-or-file-that-receives-input.c
  ```
- \>2 processes:
  ```console
  >>> ./input-program-1 | ./2-program-that-receives-input-from-1 | ./3-program-that-receives-input-from-2 | ...
  ```

## 6.3. Signals
SIGINT (`Ctrl+C`) & EOF (`Ctrl+D`) are **signals** -- type of IPC that interrupts processes; *signals are sent to processes & the process' kernel default handlers *\**{.b} either ignore the signal or terminate the process*:

- `CTRL+D` -- sends EOF (end-of-file) character to current process; signals end of input; **same as `read` returning 0 bytes reads bc it reached end of file** (*note that there is _no_ null termination to indicate EOF or end-of-string in Linux; there is only `read` returning 0 bytes*)
  - Kernel returns 0 on closed file descriptor
  - Need to check for errors (by saving `errno`)!

- `CTRL+C` -- sends SIGINT (keyboard interrupt) to current process

*\**{.b} **Default kernel handler EXIT CODE:** $128 + signal\_number$ (outputted to terminal!)

### 6.3.1. `sigaction()`
Enables setting custom signal handlers (instead of using kernel default handlers); involves declaring a function with no return (`void`) & has `int` argument of signal number.

#### 6.3.1.1. Common Signal Numbers (in Linux)
- 2: SIGINT (interrupt from keyboard)
- **9: SIGKILL (terminate immediately)** -- useful!
- 11: SIGSEGV (memory access violation)
- 15: SIGTERM (terminate)

### 6.3.2. How Signal Handlers Work
When a process receives a signal, the process pauses & then resumes after the signal handler finishes (concurrency).
- Processes can be interrupted at any point in execution.

#### 6.3.2.1. `sigaction()` Example 1
```c
// custom signal handler code
void handle_signal(int signum) {
  printf("Ignoring signal %d\n", signum);
}

// boilerplate code to set custom signal handler
void register_signal(int signum) {
  struct sigaction new_action = {0};
  sigemptyset(&new_action.sa_mask);
  new_action.sa_handler = handle_signal; // setting our custom signal handler

  // error checking
  if (sigaction(signum, &new_action, NULL) == -1) {
    int err = errno;
    perror("sigaction");
    exit(err);
  }
}

int main(void) {
  // ...

  register_signal(SIGINT); // CTRL+C
  register_signal(SIGTERM); // CTRL+D

  // ...

  return 0;
}
```

#### 6.3.2.2. `sigaction()` Example 2 (`read()` Error Handling)
Signals (e.g. SIGINT: `CTRL+C`) can cause errors by interrupting `read()` & `write()` system calls, so they need additional error handling (via checking `errno` after checking error conditional logic [i.e. `if (... = -1)`]):
```c
// modifying our `cat` example above...

  // ...

  char buffer[4096];
  ssize_t bytes_read;
  while ((bytes_read = read(0, buffer, sizeof(buffer))) != 0) {
    if (bytes_read == -1) {
      /*-------------------*/
      if (errno == EINTR) { // represents interrupted system calls
      	continue;
      /*-------------------*/
      } else {
    	break;
      }
    }

    // ...
  }

  // ...
```

### 6.3.3. Sending Signals via `kill` in the Terminal
- `>>> kill <pid>` -- sends [SIGTERM](#6211-common-signal-numbers-in-linux) to process with given pid; is ignored by default
- `>>> kill <pid> -SIGNAL_NUMBER` -- sends signal corresponding to [`SIGNAL_NUMBER`](#6211-common-signal-numbers-in-linux)
  - e.g. SIGKILL via `>>> kill -9 <pid>` terminates immediately by [default kernel handler](#63-how-signal-handlers-work) *unless process in [uninterruptible sleep](#52-process-states)*

### 6.3.4. `pidof`
Terminal command used to find pids of processes given program names.

e.g.
```console
>>> pidof ./running-program
```

## 6.4. Non-blocking Calls
Non-blocking call return immediately (allows for checking if something occurs).
- To turn [`wait` into a non-blocking call](#531-calling-wait-on-child-processes), use `waitpid()` with `WNOHANG` in options
- Can use a poll or interrupt to react to changes in non-blocking calls

### 6.4.1. Blocking vs. Non-blocking Calls
- Blocking call -- parent process is suspended until child process terminates (**including being acknowledged by `wait()` or `waitpid()`**)
- Non-blocking call -- parent process continues executing while child process terminates

### 6.4.2. `waitpid()` vs. `wait()`
- [`wait()`](#5311-wait-example)
  - waits for ANY child process to terminate
  - is ONLY a blocking call
- [`waitpid()`](#64-non-blocking-calls)
  - can be used to wait for a SPECIFIC pid of a child process
  - can be set as a non-blocking call

***Q:*** what are some usecases for `waitpid()` & `wait()`? {.lr}
> ***A:*** can set `waitpid()` or `wait()` so that a specific or any child process will always run before the next running period for the parent processe (e.g. [2022 Final Q2](#731-2022-final-q2)) {.lg}

### 6.4.3. Polling
Calling `waitpid` repeatedly until the child process exists before `wait`

```c
// wait-poll-example.c


int main() {
  pid_t pid = fork();
  if (pid == -1) {
    return errno;
  }

  // child process
  if (pid == 0) {
    sleep(2);

  // parent process
  } else {
    pid_t wait_pid = 0;
    int wstatus;

    unsigned int count = 0;

    // POLLING `waitpid()` repeatedly
    while (wait_pid == 0) {
      ++count;
      printf("Calling wait (attempt %u)\n", count);
      // set waitpid() to non-blocking call via WNOHANG
      wait_pid = waitpid(pid, &wstatus, WNOHANG);
    }

    if (wait_pid == -1) {
      int err = errno;
      perror("wait_pid");
      exit(err);
    }
    // do something on successful child process exit via `wait`
    // see #### 5.3.1.1. `wait()` Example for more details
    if (WIFEXITED(wstatus)) {
      printf("Wait returned for an exited process! pid: %d, status: %d\n", wait_pid, WEXITSTATUS(wstatus));
    } else {
      return ECHILD;
    }
  }
  return 0;
}
```

### 6.4.4. Using Interrupt Handlers
Instead of calling `wait()` or `waitpid()` in `main()`, we can do it in the interrupt handler since the kernel sends the SIGCHLD signal whenever a child process exits.
- Similar to hardware generating interrupts in the kernel
- Interrupt handler defined using [`sigaction()`](#631-sigaction)

```c
// wait-interrupt-example.c
void handle_signal(int signum) {
  // ignore non-child process exits
  if (signum != SIGCHLD) {
    printf("Ignoring signal %d\n", signum);
  }

  printf("Calling wait\n");
  int wstatus;
  // no longer need to poll since signal must be from child
  // waitpid(-1, ...) means waiting for ANY process (same as `wait()`, except as a non-blocking call bc of `waitpid()`)
  pid_t wait_pid = waitpid(-1, &wstatus, WNOHANG);
  if (wait_pid == -1) {
    int err = errno;
    perror("wait_pid");
    exit(err);
  }
  if (WIFEXITED(wstatus)) {
    printf("Wait returned for an exited process! pid: %d, status: %d\n", wait_pid, WEXITSTATUS(wstatus));
  }
  else {
    exit(ECHILD);
  }
  exit(0);
}

void register_signal(int signum) {
  struct sigaction new_action = {0};
  sigemptyset(&new_action.sa_mask);
  new_action.sa_handler = handle_signal;
  if (sigaction(signum, &new_action, NULL) == -1) {
    int err = errno;
    perror("sigaction");
    exit(err);
  }

int main() {
  register_signal(SIGCHLD);

  pid_t pid = fork();
  if (pid == -1) {
    return errno;
  }

  if (pid == 0) {
    sleep(2);
  } else {
    while (true) {
      printf("Time to go to sleep\n");
      sleep(9999);
    }
  }
  return 0;
}
```

#### 6.4.4.1. Interrupt Handlers Run to Completion
Interrupts can occur while an interrupt handler is already running, so all interrupt handler code must be reentrant:
- RENTRANT -- able to pause execution (*of 1st call to interrupt handler*), execute another call (*to 2nd call to same interrupt handler function*), & resume execution of 1st call after finishing 2nd call


#### 6.4.4.2. 3 Terms for "Interrupts" on RISC-V CPUs
- **Interrupt**
  - Triggered by external hardware
  - Handled by kernel (*needs to respond quickly*)
- **Exception**
  - Triggered by an instruction (e.g. divide-by-0, illegal memory access)
  - Default handler is kernel (calling process suspended)
  - Process can optionally handle exceptions
    - **not**{.lr} like C++ exceptions, but **hardware** exceptions
- **Trap**
  - Basically just an interrupt handler
  - Transfer of control to a trap handler caused by either an exception or an interrupt
    - e.g. system calls are *requested* traps
      - because system call is an instruction so it would generate an exception to be handled by the kernel (e.g. `read()`, `write()`, `open()`)
      - "I want the kernel to run some specific code"

## 6.5. PRACTICE

***Q:*** what does file descriptor 0 represent by default? {.lr}
> ***A:*** standard input (to terminal). {.lg}

---

***Q:*** what happens if we read from file descriptor 1? {.lr}
> ***A:*** indeterminate behaviour; file descriptor 1 is for writing, so this shouldn't be done but if it was then it might act as file descriptor 0 (read) or it could fail. {.lg}

---
> ---

***Q: a)*** how to use shell to redirect output from one program (`a.exe`) as input to another program (`b.exe`)? {.lr}
> ***A:*** `>>> ./a.exe < ./b.exe` {.lg}

> ---

***Q: b)*** how to use shell to redirect output from one program (`a.exe`) as input to another program (`b.exe`), *and use output from `b.exe` as input to `c.exe*? {.lr}
> ***A:*** `./a.exe | ./b.exe | ./c.exe` {.lg}

> ---

***Q:*** how to get the exit code $c$ of a process given a terminal exit code $x$? {.lr}
> ***A:*** $c = 128 - x$ {.lg}

---

***Q:*** what type of OS concept is used in signal handling? {.lr}
> ***A:*** concurrency; switching between running processes to simulate simulataneous execution. {.lg}

---

***Q:*** what happens to child processes after a process is killed via `kill -9 <pid>`? {.lr}
> ***A:*** since parent is being terminated first, [orphan child processes](#533-orphan-process) get reparented by [`init`](#521-processkernel-startup-via-init), which continually terminates all orphan processes. {.lg}

---
> ---

***Q: a)*** how to make continuous polling (for `waitpid()` in a loop) less resource-intensive w/o using interrupts? {.lr}
> ***A:*** add a delay (e.g. $1 \frac{poll}{second}$) {.lg}

```c
  // ...
  // e.g. delayed polling
  while (wait_pid == 0) {
    sleep(1)
    wait_pid = waitpid(pid, &wstatus, WNOHANG);
  }
  // ...
```

> ---

***Q: b) what are the tradeoffs of excluding vs. adding the delay?***  {.lr}
> ***A:*** adding the delay means less resource usage at the expense of response time; excluding the delay means faster response time at the expense of waste of resources. {.lg}

> ---
---









<!--------------------------------{.gray}------------------------------>







<hr style="border:30px solid #FFFF; margin: 100px 0 100px 0; {.gray}"> </hr>






<!--------------------------------{.gray}------------------------------>
<div style="page-break-after: always;"></div>

# 7. Process Practice (2023-09-21)
## 7.1. Multiprogramming
- **UNI**programming
  - only one process running at a time
  - multiple processes **not** running in parallel or concurrently
- **MULTI**programming
  - allows multiple processes (can run in parallel OR concurrently)

### 7.1.1. Scheduler
Before a process is created but after a signal has been to the OS to create it, the process is in the [waiting state](#52-process-states) until it is loaded into memory.
- While waiting, the scheduler decides when to run the process

### 7.1.2. How Switching/Swapping Processes Works (via Core Scheduling Loop)
```mermaid
graph LR;
  A(Pause current process) --> B(Save state);
  B --> C(Get next process from scheduler);
  C --> D(Load next process state and run);
  D --> E(Receive request for new process)
  E --> A
```

### 7.1.3. COOPERATIVE vs. TRUE Multitasking
We can let each process indicate when it can be paused OR have the OS pause processes itself:
- **COOPERATIVE** Multitasking -- processes use a system call to tell OS to pause it
- **TRUE** Multitasking -- OS retains control over pausing processes
  - OS gives processes set time slices
  - OS can wake up periodically using interrupts to do scheduling (instead of spending all clock cycles scheduling)


### 7.1.4. Context Switching = Swapping Processes
- At minimum requires saving all current registers of process
  - Need to save all values **using the same CPU that is being saved**
- Context switching is pure overhead; need to be as fast as possible

## 7.2. `pipe()`
```c
int pipe(int pipefd[2])
```
- Returns:
  - `0` -- on success (*created* 2 file descriptors)
  - `-1` -- on failure (sets `errno`; *couldn't create* 2 file descriptors)
- Forms a one-way communication channel using 2 file descriptors
  - `pipefd[0]` -- read end of pipe
  - `pipefd[1]` -- write end of pipe
- e.g. [`|` forms a pipe between 2 processes](#62-redirecting-standard-file-descriptors-using-the-shell)

```mermaid
graph LR;
  1["pipefd[1]"] -->|writes to| 2["pipefd[0]"]
```

Can think of `pipe()` as a kernel-managed buffer
- Kernel handles memory allocation, etc.
- We only interface with writing to one end & reading from other end.

### 7.2.1. `pipe()` Example

```c
// pipes.c

// error handler
void check(int ret, const char* message) {
    if (ret != -1) { return; }
    int error = errno;
    perror(message);
    exit(error);
}

int main(void) {
  // file descriptor array of size 2 for `pipe()`
  int fds[2];
  // initialize pipe via `pipe(fds)`
  check(pipe(fds), "pipe");

  pid_t pid = fork();
  check(pid, "fork");

  // parent
  if (pid > 0) {
    const char* str = "Hello from parent to child";
    int len = strlen(str);
    // write `str` to write end of pipe (`fds[1]`)
    int bytes_written = write(fds[1], str, len);
    check(bytes_written, "write");

  // child
  } else {
    char buffer[4096];
    // read end of pipe (`fds[0]`)
    int bytes_read = read(fds[0], buffer, sizeof(buffer));
    check(bytes_read, "read");
    printf("Child reads: %.*s\n", bytes_read, buffer);
  }

  // REMEMBER TO CLOSE PIPE ENDS!
  close(fds[0]);
  close(fds[1]);

  return 0;
}
```

***Q:*** what happens to the child process if we remove the `write()` call in the parent process? {.lr}
> ***A:*** the child process will block indefinitely on the `read()` call since it will not receive any data from that end of the pipe. {.lg}
  - Moreover, since nothing will happen in the parent process, after the parent process finishes the child will become an orphan & get reparented to `init` (where it will continue waiting for read data)

---

***Q:*** what are the values of `fds[0]` & `fds[1]` in the code above? {.lr}
> ***A:*** **file descriptors 0, 1, 2 (open, read, write) already exist, so the kernel created file descriptors starting at the next lowest number (3);** `fds[0]` = 3 (read end of pipe) & `fds[1]` = 4 (write end of pipe) {.lg}
  > Note that at the time of the `fork()`, all variables **INCLUDING FILE DESCRIPTORS**{.p} are copied from the parent to the child process

---

***Q:*** does this mean that the parent & child process refer to different file descriptors wrt pipe? {.lr}
> ***A:*** no; use of pipe is identical in parent & child processes {.lg}

---

***Q:*** what is output if we modify the code as below, and why? {.lr}
```c
  // ...

  // parent
  if (pid > 0) {
    const char* str = "Hello from parent to child";
    int len = strlen(str);
    // write `str` to write end of pipe (`fds[1]`)
    int bytes_written = write(fds[1], str, len);
    check(bytes_written, "write");
    // ---------------------------
    close(fds[0]) // read
    close(fds[1]) // write
    // ---------------------------

  // child
  } else {
    // ---------------------------
    close(fds[1]) // write
    // ---------------------------
    char buffer[4096];
    // read end of pipe (`fds[0]`)
    int bytes_read = read(fds[0], buffer, sizeof(buffer));
    check(bytes_read, "read");
    printf("Child reads: %.*s\n", bytes_read, buffer);
    // ---------------------------
    close(fds[0]) // read
    // ---------------------------
  }

  // ...
```
> ***A:*** prints `Child read:          ` {.lg}
- `read()` is able to receive 0 bytes so it does not wait indefinitely (unlike in previous example)
- works because the kernel keeps track of how many processes have a file descriptor that refer to the write end of the pipe; if `read()` is called on a (read) file descriptor & it is not possible for that pipe to read any more data (because it was closed), then the kernel sends 0 bytes to close that (read) file descriptor

## 7.3. Using `&` in Shell
Starts a given process & outputs pid on finish
e.g.
```console
>>> sleep 10 &
[1] 57827

>>> # ...wait 10 s...
[1] * 57827 done     sleep 1

>>>
```

## 7.4. PRACTICE

### 7.4.1. 2022 Final Q2

***Q:*** For each program shown below, state whether it will produce the same output each time it is run, or whether it may produce different outputs when run multiple times. Explain why the program behaves like this. {.lr}
- a){.lr}
  ```c
  int main() {
    int i = 4;
    while (i != 0) {
      int pid = fork();
      if (pid == 0) {
        i--;
      } else {
        printf("%d\n", i);
        exit(0);
      }
    }
    return 0;
  }
  ```
- ***A:*** `pid == 0` is child process code {.lg}
  - each time `fork()` is called, a child process is created with a copy of `i`.
  - the kernel non-deterministically decides whether to run the parent or child process first, so there could be different outputs each time the program is ran.
  - <!-- REPLACE BELOW WITH CORRECTM NESTED MERMAID DIAGRAM -->
  - e.g. 1: `fork()` 1 -> parent (`print 4`) -> child (`i = 3`) -> `fork()` 2 -> parent (`print 3`) -> child (`i = 3`) -> ...
    ```console
    4
    3
    ...
    ```
  - vs. e.g. 2: `fork()` 1 -> child (`i = 3`) -> parent (`print 3`) ->  `fork()` 2 -> parent (`print 3`) -> ...
    ```console
    3
    3
    ...
    ```

- b){.lr}
  ```c
  int main() {
    int i = 4;
    while (i != 0) {
      int pid = fork();
      if (pid == 0) {
        i--;
      } else {
        waitpid(pid, NULL, 0);
        printf("%d\n", i);
        exit(0);
      }
    }
    return 0;
  }
  ```
- ***A:***  {.lg}
  - [`waitpid(..., ..., 0)`](#642-waitpid-vs-wait) means that the parent process waits for (i.e. is "blocked" by) the child process to exit before running.
  - as a result, the child process code will always run before the parent process code every iteration of the loop
  - since printing is in parent process code, this means each process will `fork()` until `i == 0`, at which point the deepest-nested child process exits & its parent runs (printing `i == 1`), thus printing `1 2 3 4`
  - `fork()` 1 -> child (`i = 3`) ->  -> parent (`print 3`) -> `fork()` 2 -> child (`i = 2`) -> ...
    ```console
    3
    2
    1
    0
    ```

***Q:*** does it matter whether pipe is called before or after forking? What would be different in both cases? {.lr}
> ***A:*** {.lg}
  - Because when you fork, the file descriptors are copied in the child, so both the parent and child can access the same things through their independent file descriptors.
    - The memory for the pipe exists in the kernel, and you can only access it through the file descriptors returned by pipe.
    - So when the fork happens, the kernel copies everything, including all the file descriptors and what they "point to" or what they represent.
    - So if the pipe is before the fork, both processes would have the same file descriptors pointing to the same thing
  - If pipe is after fork, both processes would make independent pipes, and they wouldn't share anything
    - They're independent after the fork, so if one process closes file descriptor 3, it doesn't close it for the other process








<!--------------------------------{.gray}------------------------------>







<hr style="border:30px solid #FFFF; margin: 100px 0 100px 0; {.gray}"> </hr>






<!--------------------------------{.gray}------------------------------>
<div style="page-break-after: always;"></div>

# 8. Subprocess (2023-09-22)
## 8.1. Lab 2 Goals
- Create a new process that launches the command line argument
- Send the string `Testing\n` to that process
- Receive any data it writes to standard output

## 8.2. Easier to Use C APIs
### 8.2.1. `execlp()`
More convenient alternative to `execve()`
```c
int execlp(const char *file, const char *arg /* ..., (char *) NULL */);
```
- Returns:
  - Does not return on success
  - ...`-1` on failure
- Allows for skipping use of string arrays via C varargs
  - 1st argument `const char *file` does not need to be a path to a file, can simply be program name
  - Can handle any number of arguments via C varargs (`const char *arg`)
- Will search executables using directories under the `PATH` environment variable

### 8.2.2. `dup()` & `dup2()`
Creates a new file descriptor that refers to the object described by a given file descriptor
```c
int dup(int oldfd)
int dup2(int oldfd, int newfd);
```
```mermaid
graph LR;
  1["newfd"] -->|points to| 2["oldfd"]
```
- Returns:
  - ...a new file descriptor on success
  - ...`-1` on failure
- `dup()` returns the lowest file descriptor available
- `dup2()` closes the `newfd` argument if open (i.e. if its a valid file descriptor) & then sets `newfd` to refer to the `oldfd`
  - useful so you don't have to close `newfid` before calling `dup2()`

## 8.3. Subprocess Example
### 8.3.1. Skeleton
```c
// subprocess.c

#include <assert.h>
#include <errno.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/wait.h>
#include <unistd.h>

static void check_error(int ret, const char *message) {
    if (ret != -1) {
        return;
    }
    int err = errno;
    perror(message);
    exit(err);
}

static void parent(int in_pipefd[2], int out_pipefd[2], pid_t child_pid) {
}

static void child(int in_pipefd[2], int out_pipefd[2], const char *program) {
    execlp(program, program, NULL);
}

int main(int argc, char* argv[]) {
    if (argc != 2) {
        return EINVAL;
    }

    int in_pipefd[2] = {0};

    int out_pipefd[2] = {0};

    pid_t pid = fork();
    if (pid > 0) {
        parent(in_pipefd, out_pipefd, pid);
    } else {
        child(in_pipefd, out_pipefd, argv[1]);
    }

    return 0;
}
```

### 8.3.2. Tasks To Do
- create pipe (before `fork()`)
- modify file descriptor to allow reading from `stdout = 1` (write) via `dup2()`
- close file descriptors
- modify file descriptors to allow writing to `stdout = 0` (read)

### 8.3.3. Completed Code
```c
#include <assert.h>
#include <errno.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/wait.h>
#include <unistd.h>

#define STDIN 0 // == STDIN_FILENO
#define STDOUT 1 // == STDOUT_FILENO
#define STDERR 2 // == STDERR_FILENO

#define READ 0
#define WRITE 1

static void check_error(int ret, const char *message) {
    if (ret != -1) {
        return;
    }
    int err = errno;
    perror(message);
    exit(err);
}

static void child(int in_pipefd[2], int out_pipefd[2], const char *program) {
  // 0: stdin
  // 1: stdout
  // 2: stderr
  // 3: output_pipefd[0] = read end of pipe
  // 4: output_pipefd[1] = write end of pipe

  // modify fds so stdin redirects to input of pipe used to input something to output pipe...
  // ---> take the "file" pointed to by `in_pipefd[READ]` & make STDIN point to it
  check_error(dup2(in_pipefd[READ], STDIN), "dup2");
  close(in_pipefd[READ]);
  close(in_pipefd[WRITE]);

  // ...and so stdout redirects to write to pipe used to read some output
  // ---> take the "file" pointed to by `out_pipefd[WRITE]` & make STDOUT point to it
  check_error(dup2(out_pipefd[WRITE], STDOUT), "dup2");
  close(out_pipefd[READ]);
  close(out_pipefd[WRITE]);
  // 0: stdin --> read end of pipe
  // 1: stdout --> write end of pipe
  // 2: stderr
  // 3: output_pipefd[0] = read end of pipe
  // 4: output_pipefd[1] = write end of pipe

  execlp(program, program, NULL);
}

static void parent(int in_pipefd[2], int out_pipefd[2], pid_t child_pid) {
  close(in_pipefd[READ]); // we are not reading from the pipe used to input something
  close(out_pipefd[WRITE]); // we are not writing to the pipe used to read some output

  // write to the input pipe
  const char* message = "Testing\n";
  ssize_t bytes_written = write(in_pipefd[WRITE], message, strlen(message));
  check_error(bytes_written, "write");
  close(in_pipefd[WRITE]); // close input pipe after writing

  // wait for child process to exit via `waitpid`
  int wstatus;
  check_error(waitpid(child_pid, &wstatus, 0), "wait");
  assert(WIFEXITED(wstatus));
  assert(WEXITSTATUS(wstatus) == 0);

  // output pipe reads from stdout now
  char buffer[4096];
  ssize_t bytes_read = read(out_pipefd[READ], buffer, sizeof(buffer));
  check_error(bytes_read, "read");
  printf("Got: %.*s", (int) bytes_read, buffer);
  close(out_pipefd[READ]); // close output pipe after reading
}

int main(int argc, char* argv[]) {
  if (argc != 2) {
    return EINVAL;
  }

  int in_pipefd[2] = {0};
  check_error(pipe(in_pipefd), "in_pipe");

  int out_pipefd[2] = {0};
  check_error(pipe(out_pipefd), "out_pipe");

  pid_t pid = fork();
  if (pid > 0) {
    parent(in_pipefd, out_pipefd, pid);
  } else {
    child(in_pipefd, out_pipefd, argv[1]);
  }

  return 0;
}
```

#### 8.3.3.1. Visualization of Pipes
```mermaid

```

<div align="right">
<table><td>
<a href="#start-of-content">👆 Scroll to top</a>
</td></table>
</div>