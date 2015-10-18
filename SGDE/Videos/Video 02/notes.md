# Video 02 Notes

## Symbol Files

#### What do Symbol Files tell us?

- ```info sources``` - shows source code files which gdb will attempt to load.
- ```info variables``` - shows all global and static variables.
- ```info functions``` - shows all defined function prototypes.
- ```info scope``` - shows all scopes available in the program.
- ```info scope FUNCTION_NAME``` - shows all local variables in function specified. 
- ```maint print symbols FILENAME```

#### Source Code vs Symbol Files

- Source code is not kept in the symbol files.
- Symbol files can contain reference to source code location.
- ```list``` command is useful when you have source code that is being referenced.


#### Copy Symbol Files off of a Binary

- ```objcopy``` allows you to create a symbol file from a binary with symbols included.
- syntax: ```objcopy --only-keep-debug SRC_BINARY_FILE DEST_SYMBOL_FILE```
- The symbol files remain in the original binary.


#### Stripping Symbol Files off of a Binary

- ```strip``` removes symbol files from a binary.
- syntax: ```strip --strip-debug BINARY_TO_STRIP```
- Leaves only name of functions.
- to remove absolutely everything, add the ```--strip-unneeded ``` flag

## Symbol Files in Security

#### Developers

- Developers should not ship products with symbol files.
- When customer is debugging, developers can ship symbol files seperately.

#### Loading Symbol Files

- You can load symbol files that are not built into the binary.
- At gdb prompt: ```symbol-file DEBUG_SYMBOL_FILE```

#### Adding Symbol Files Back to a Binary

- You can add symbol files back into the binary file.
- syntax: ```objcopy --add-gnu-debuglink=DEBUG_SYMBOL_FILE DEST_BINARY```


---
 
[Back to main](https://github.com/rot0xd/SecurityTube/blob/master/SGDE/README.md)
