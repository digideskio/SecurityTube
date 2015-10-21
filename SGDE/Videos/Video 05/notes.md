# Video 05 Notes

## Breakpoints, Examining Registers and Memory

#### What is a breakpoint?
- Used to "pause" a program during execution
- Can set a breakpoint on certain criteria, such as before an instruction executes.
- While "paused", the debugger allows you to inspect/modify registers, memory, etc

#### Sample Program

```
#include <stdio.h>
#include <string.h>

void echoInput(char *userInput){
  char buffer[20];
  strcpy(buffer, userInput);
  printf("\n\n%s\n\n", buffer);
}

int main(int argc, char **argv){
  echoInput(argv[1]);
  return 0;
}
```

#### Useful commands in ```gdb```
- ```(gdb) file PROGRAM``` loads PROGRAM into the debugger
- ```(gdb) set args ARGS``` sets the command line arguments to ARGS
- ```(gdb) set args "`CMD`"``` sets the command line arguments to output of CMD command.
- ```(gdb) run``` runs the program in the debugger 
- ```(gdb) break FUNCTION``` sets a breakpoint at FUNCTION in the program.
- ```(gdb) break *0xFFFFFFFF``` sets a breakpoint at memory address 0xFFFFFFFF in the program.
- ```(gdb) disable 1``` disables the first breakpoint.
- ```(gdb) enable 1``` enables the first breakpoint.
- ```(gdb) delete 1``` deletes the first breakpoint.
- ```(gdb) info breakpoints``` lists all the breakpoints currently set.
- ```(gdb) list``` displays the source code if available
- ```(gdb) info functions``` displays the functions available to the program.
- ```(gdb) info registers``` displays the current values in the registers.
- ```(gdb) set $eip = &secretFunction``` sets the next instruction to the address of secretFunction.
- ```(gdb) help x``` displays different ways to examing values in registers/memory
- ```(gdb) disassemble FUNCTION``` prints the disassembly of FUNCTION's assembly code.
- ```(gdb) continue``` continues from a breakpoint back to normal program flow. 
- ```(gdb) step N``` steps over N lines of code in the program.
- ```(gdb) stepi N``` steps over N assembly instructions in the program.

---
 
[Back to main](https://github.com/rot0xd/SecurityTube/blob/master/SGDE/README.md)
