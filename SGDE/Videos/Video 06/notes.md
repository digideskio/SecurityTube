# Video 06 Notes

## Modifying Registers and Memory

#### Modify Data in Memory
- ```(gdb) set {char}0xFFFFFFFF = 'B'``` sets the char at 0xFFFFFFFF to 'B'
- ```(gdb) set {int}0xFFFFFFFF = 67``` sets the int at 0xFFFFFFFF to 167

#### Modify CPU Registers
- ```(gdb) set $eax = 10``` sets the eax register to 10
- ```(gdb) set $eip = &FUNCTION``` sets the instruction pointer to FUNCTION's address

---
 
[Back to main](https://github.com/rot0xd/SecurityTube/blob/master/SGDE/README.md)
