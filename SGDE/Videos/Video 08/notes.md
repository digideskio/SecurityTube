# Video 08 Notes

## Cracking a Simple Binary with Debug Symbols

#### Strings
- Displays strings in the program
- Poorly coded programs may reveal secret information
- Secret can be easily hidden by encoding or encrypting.
- Not very powerful, but worth checking.


#### Runtime Analysis
- Debug symbols make things easier
- ```(gdb) info functions``` displays the functions available to the program
- ```(gdb) info variables``` displays the global variables of the program 
- ```(gdb) info scope FUNCTION``` displays the variables local to the scope of FUNCTION

---
 
[Back to main](https://github.com/rot0xd/SecurityTube/blob/master/SGDE/README.md)
