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
- [3. Libraries (2023-09-13](#3-libraries-2023-09-13)
  - [3.1. Types](#31-types)


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




------------------------------{.gray}------------------------------>






<hr style="border:30px solid #FFFF; margin: 100px 0 100px 0; {.gray}"> </hr>






<!--------------------------------{.gray}------------------------------>
<div style="page-break-after: always;"></div>

# 3. Libraries (2023-09-13
## 3.1. Types

integers -- signed (default) or unsigned (- 1 bit)
- int32 bits
- short 16 bits
- long int (>=32 bits)

real
- float
- double
- long double

text
- char (1 byte) -- 'a'
- NOT string -- "ab" {.lr}

logic
- bool

void