# Video 10 Notes

## Conditional Breakpoints using Variables and Registers

#### Conditional Breakpoints
- Break only if condition is met.
- Handy in cases where there are loops.
- Conditions can be simple or complex.

#### Setting a Conditional Breakpoint
- If you have the source:
  - ```(gdb) break 10``` sets a breakpoint at line 10.
  - ```(gdb) condition 1 VARIABLE == 5``` stops at breakpoint 1 only if VARIABLE is 5.
- If you do not have the source:
  - ```(gdb) break *0xFFFFFFFF``` sets a breakpoint at address 0xFFFFFFFF
  - ```(gdb) condition 1 $eax != 0``` stops at breakpoint 1 only if eax does not contain 0.

---
 
[Back to main](https://github.com/rot0xd/SecurityTube/blob/master/SGDE/README.md)
