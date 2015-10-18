#### GDB commands

To display common registers:

```
(gdb) info registers
```

To display all registers:

```
(gdb) info all-registers
```

To display assembly in intel syntax:

```
(gdb) set disassembly-flavor intel
```

To view the memory layout of a process:

```
(gdb) info proc mappings
```

To view a list of functions in the loaded binary:

```
(gdb) info functions
```

To have gdb display a register at each breakpoint/stopping point:

```
(gdb) display /x $eax
(gdb) display /x $ebx
(gdb) display /x $ecx
```

To have gdb perform a set of tasks at each breakpoint/stopping point:
```
(gdb) define hook-stop
Type commands for definition of "hook-stop".
End with a line saying just "end".
>x/8xb &sample
>i r eax
>i r ebx
>i r ecx
>end
```

#### CPU Modes

- Real Mode
  - The mode at power/rest
  - Can only access 1MB memory
  - No memory protection/privilege levels

- Protected Mode
  - Up to 4GB memory
  - Introduces memory protection/privilege levels
  - Supports Virtual-8086 mode

- System Management Mode
  - Used for power management taskes

We only focus on protected mode for this course

#### Process Memory Layout

| Memory Section   | Contents                               |
|------------------|----------------------------------------|
| 0xFFFFFF         |                                        |
| Stack            | Function arguments and local variables |
| Heap             | Dynamically allocated memory           |
| BSS              | Uninitialized data                     |
| Data             | Initialized data                       |
| Text             | Program code                           |
| 0x000000         |                                        |


To view the memory layout of a process from the command line:

```
cat /proc/$PID/maps
pmap $PID
```


#### Building and running assembly

To compile assembly into an object file for use in an elf32:

```
nasm -f elf32 -o HelloWorld.o HelloWorld.asm 
```

To link the object file into an executable:

```
ld -o HelloWorld HelloWorld.o
```

Basic HelloWorld.asm:

```
; HelloWorld.asm
; Author: rot0xd

global _start

section .text

  _start:
    ; Print message.
    mov eax, 0x4
    mov ebx, 0x1
    mov ecx, message
    mov edx, messageLength
    int 0x80

    ; Exit gracefully.
    mov eax, 0x1
    mov ebx, 0x0
    int 0x80

section .data
  message:        db "Hello World!"
  messageLength   equ $-message
```
