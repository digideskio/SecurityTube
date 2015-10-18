# Video 03 Notes

## Inspecting Symbols with nm

#### Sample nm Output

```
root@kali:~# nm a.out 
080495c0 d _DYNAMIC
080496b4 d _GLOBAL_OFFSET_TABLE_
0804851c R _IO_stdin_used
         w _ITM_deregisterTMCloneTable
         w _ITM_registerTMCloneTable
.
.
.
.
08048390 t deregister_tm_clones
08048420 t frame_dummy
0804844c T main
         U printf@@GLIBC_2.0
080483c0 t register_tm_clones
         U strlen@@GLIBC_2.0
```

#### nm Output Fields

| Virtual Address | Symbol Type | Symbol Name                  |
|-----------------|-------------|------------------------------|
| 080495c0        | d           | _DYNAMIC                     |
| 080496b4        | d           | _GLOBAL_OFFSET_TABLE_        |
| 0804851c        | R           | _IO_stdin_used               |
|                 | w           | _ITM_deregisterTMCloneTable  |
| 0804844c        | T           | main                         |


#### nm Symbol Types

| Symbol Type | Meaning                        |
|-------------|--------------------------------|
| A           | Absolute Symbol                |
| B           | Uninitialized Data (BSS)       |
| D           | Initialized Data               |
| N           | Debugging Symbol               |
| T           | Text Section                   |
| U           | Symbol Undefined Right Now     |

- Lower case is a local symbol
- Upper case is external

---
 
[Back to main](https://github.com/rot0xd/SecurityTube/blob/master/SGDE/README.md)
