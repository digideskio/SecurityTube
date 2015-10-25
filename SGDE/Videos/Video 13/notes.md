# Video 13 Notes

## iPhone Application Cracking with GDB

#### Breaking Jailbreak Detection
- iOS Applications vulnerable to piracy.
- Checking for jailbreaking is common by developers.

#### Debugging iOS Applications
- Use ```class-dump-z``` to display all objects in an application.
- ```(gdb) break -[AntiPiracyViewController isJailbroken]``` breaks at the isJailbroken function of the AntiPiracyViewController class.

---
 
[Back to main](https://github.com/rot0xd/SecurityTube/blob/master/SGDE/README.md)
