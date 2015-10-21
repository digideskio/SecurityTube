# Video 07 Notes

## Convenience Variables and Calling Routines

#### Convenience Variables
- You can create variables in GDB to hold data
- ```(gdb) set $i = 10``` creates a variable named 'i' that holds the value 10
- ```(gdb) set $dyn = (char *)malloc(10)``` allocates 10 bytes of memory and stores the address in variable 'dyn'
- ```(gdb) $demo = "vivek"``` stores the string 'vivek' in variable named 'demo'
- ```(gdb) set argv[1] = $demo``` replaces address stored in argv[1] with the address of 'demo'.


#### Calling Routines
- You can also call all functions available to the program you are debugging.
- ```(gdb) info functions``` shows all callable functions from the debugger.
- ```(gdb) call strcpy($dyn, "NEW_STRING")``` calls ```strcpy``` as if it were run in the program.

---
 
[Back to main](https://github.com/rot0xd/SecurityTube/blob/master/SGDE/README.md)
