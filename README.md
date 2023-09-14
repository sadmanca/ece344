- [2023-09-07 | 1. Why Operating Systems](#2023-09-07--1-why-operating-systems)
  - [Core Operating Systems Concepts:](#core-operating-systems-concepts)
  - [Code example](#code-example)
- [2023-09-18 | 2. Kernels](#2023-09-18--2-kernels)
  - [instruction set architecture (ISA)](#instruction-set-architecture-isa)
  - [Inter-Process Communication (IPC)](#inter-process-communication-ipc)
  - [OS system calls](#os-system-calls)
    - [`write()`](#write)
    - [`exit_group()`](#exit_group)
    - [Standard File Descriptors](#standard-file-descriptors)
- [2. Intro to C++](#2-intro-to-c)
  - [2.1. Types](#21-types)


<!--------------------------------{.gray}------------------------------>






<hr style="border:30px solid #FFFF; margin: 100px 0 100px 0; {.gray}"> </hr>






<!--------------------------------{.gray}------------------------------>

<div style="page-break-after: always;"></div>

# 2023-09-07 | 1. Why Operating Systems

Pre-requisites:
- C programming and debugging
- Converting between bianry, hex, decimal
- Little-endian, big-endian
- Byte-addressable memory, memory address ala pointers

---

## Core Operating Systems Concepts:
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

## Code example


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














# 2023-09-18 | 2. Kernels

## instruction set architecture (ISA)
refers to machine code that a CPU understands. 3 main ISAs in use today:
- `x86-64 / amd64` - desktops
- `aarch64 / arm64` - mobile
- `riscv / rv64gc` - open source ARM alternative

## Inter-Process Communication (IPC)
- IPC -- mechanism that allows OS to transfer data between processes

- File descriptor -- **not just a file**; a resource that users can either read bytes from or write bytes to; is identified by an index stored in a process
  - e.g. .txt file, ANY file, **terminal**

## OS system calls
C functions that operate on/using the OS

### `write()`
Writes bytes from byte array to file descriptor
```c
ssize_t write(int fd, const void *buf, size_t count)
// fd - file descriptor
// buf - address of start of byte array (i.e. BUFFER)
// count - number of bytes to write from buffer
```

### `exit_group()`
Exits the current process and sets an exit status code (0 status code = no errors, is why `main()` has `return 0`)
```c
void exit_group(int status)
// status - exit status code (0-255)
```

### Standard File Descriptors
- `0` / `stdin` -- standard input (read)
- `1` / `stdout` -- standard output (write)
- `2` / `stderr` -- standard error (**write**{.b})



------------------------------{.gray}------------------------------>






<hr style="border:30px solid #FFFF; margin: 100px 0 100px 0; {.gray}"> </hr>






<!--------------------------------{.gray}------------------------------>
<div style="page-break-after: always;"></div>

# 2. Intro to C++
## 2.1. Types

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