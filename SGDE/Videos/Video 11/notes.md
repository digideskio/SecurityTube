# Video 11 Notes

## Installing Debian ARMEL in QEMU

#### Download and Install QEMU
- Download from ```http://wiki.qemu.org/download/qemu-1.2.0.tar.bz2```
- ```./configure --target-list=arm-softmmu``` configures qemu for ARM architecture.
- ```make && make install``` installs qemu.

#### Download Debian ARMEL Images
- Download from ```http://people.debian.org/~aurel32/qemu/armel```
- Required files:
  - ```debian_squeeze_armel_standard.qcow2```
  - ```initrd.img-2.6.32-5-versatile```
  - ```vmlinuz-2.6.32-5-versatile```
- ```LaunchVM.sh``` is a helper script available with course materials.
  - ```qemu-system-arm``` binary which launches the image.
  - Run with flags:
    - ```-M versatilepb```
    - ```-kernel vmlinuz-2.6.32-5-versatile```
    - ```-initrd initrd.img-2.6.32-5-versatile```
    - ```-hda debian_squeeze_armel_standard.qcow2```
    - ```-append "root=/dev/sda1/"```
    - ```-m 256```
    - ```-redir tcp:2222::22```

#### ARM vs x86
- Registers are r0-r12 instead of eax, ebx, ecx, etc.
- ARM calling convention is not the same as x86.
- ARM assembly language is different than x86 as well.

---
 
[Back to main](https://github.com/rot0xd/SecurityTube/blob/master/SGDE/README.md)
