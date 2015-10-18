# Video 01 Notes

## Course Introduction and Debugging Basics

#### Lab Setup

- Ubuntu 12.04 Desktop x86
- Ubuntu 12.04 Desktop x64
- Debian ARM


#### Ubuntu VM Setup 

- **Required Packages**

```
sudo apt-get install ssh
sudo apt-get install build-essential
sudo apt-get install make
sudo apt-get install libglib2.0-dev
```

---

## What is Debugging?


#### Debugger

- Program to analyze and debug other programs

- Examples of debuggers:
  - GDB
  - IDB
  - SoftIce
  - WinDBG

#### Debugger Symbols

- Information about variables, functions, etc
- Read by the debugger to make debugging easier to understand
- Can be part of binary or shipped seperately

- To compile with debugging symbols, use gcc's ```-g``` flag.


---
 
[Back to main](https://github.com/rot0xd/SecurityTube/blob/master/SGDE/README.md)
