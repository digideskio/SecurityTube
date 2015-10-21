# Video 04 Notes

## System Call Tracing with ```strace```

#### The ```strace``` Tool
- Helper tool to understand how your program interacts with the OS.
- Traces all syscalls made by a program.
- Tells us about arguments passed and has great filtering capabilities.


#### Useful Flags
- ```-o``` - Saves output to a file
- ```-t``` - Display timestamps next to syscalls
- ```-r``` - Display relative timestamps next to syscalls
- ```-e``` - Display only the syscalls specified
- ```-p``` - Attach ```strace``` to a running process.
- ```-c``` - Displays summary of syscall statistics upon program completion 


#### Sample Normal ```strace``` Output

```
root@kali:~# strace ./helloWorld
execve("./helloWorld", ["./helloWorld"], [/* 44 vars */]) = 0
brk(0)                                  = 0x80fa000
access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
mmap2(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0xb77c4000
access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
open("/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
fstat64(3, {st_mode=S_IFREG|0644, st_size=106467, ...}) = 0
mmap2(NULL, 106467, PROT_READ, MAP_PRIVATE, 3, 0) = 0xb77aa000
close(3)                                = 0
access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
open("/lib/i386-linux-gnu/i686/cmov/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\1\1\1\3\0\0\0\0\0\0\0\0\3\0\3\0\1\0\0\0\300\233\1\0004\0\0\0"..., 512) = 512
fstat64(3, {st_mode=S_IFREG|0755, st_size=1738492, ...}) = 0
mmap2(NULL, 1743484, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0xb7600000
mmap2(0xb77a4000, 12288, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1a4000) = 0xb77a4000
mmap2(0xb77a7000, 10876, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0xb77a7000
close(3)                                = 0
mmap2(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0xb75ff000
set_thread_area({entry_number:-1, base_addr:0xb75ff940, limit:1048575, seg_32bit:1, contents:0, read_exec_only:0, limit_in_pages:1, seg_not_present:0, useable:1}) = 0 (entry_number:6)
mprotect(0xb77a4000, 8192, PROT_READ)   = 0
mprotect(0xb77e9000, 4096, PROT_READ)   = 0
munmap(0xb77aa000, 106467)              = 0
fstat64(1, {st_mode=S_IFCHR|0600, st_rdev=makedev(136, 4), ...}) = 0
mmap2(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0xb77c3000
write(1, "Hello World!\n", 13Hello World!
)          = 13
exit_group(13)                          = ?
+++ exited with 13 +++
```

#### Sample Filtering ```strace``` Output

```
root@kali:~# strace -e open ./helloWorld
open("/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
open("/lib/i386-linux-gnu/i686/cmov/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
Hello World!
+++ exited with 13 +++
```


#### Sample Statistics ```strace``` Output

```
root@kali:~# strace -c ./helloWorld 
Hello World!
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
  0.00    0.000000           0         1           read
  0.00    0.000000           0         1           write
  0.00    0.000000           0         2           open
  0.00    0.000000           0         2           close
  0.00    0.000000           0         1           execve
  0.00    0.000000           0         3         3 access
  0.00    0.000000           0         1           brk
  0.00    0.000000           0         1           munmap
  0.00    0.000000           0         2           mprotect
  0.00    0.000000           0         7           mmap2
  0.00    0.000000           0         3           fstat64
  0.00    0.000000           0         1           set_thread_area
------ ----------- ----------- --------- --------- ----------------
100.00    0.000000                    25         3 total

```

---
 
[Back to main](https://github.com/rot0xd/SecurityTube/blob/master/SGDE/README.md)
