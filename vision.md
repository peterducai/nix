# VISION

## Ideas from other OS

### OpenBSD

* Kernel

### Linux

* Selinux

### Solaris

* RBAC
* Bootadm
* ZFS

**backwards ABI compatibility**

```
Specific Criteria for Source Compatibility:
1) General Source Code Guidelines for Eligible Applications:
• must be written to comply with the standards as listed in standards(5);
• must not be converting 32 bit applications to 64 bit applications or vice versa;
• must not include Makefiles for building object files from compiled applications to run on
specific platforms;
• must not include 3rd party software libraries (binaries) or other programming interfaces;
• must not include Assembler code in any form.
2) Compiler Guidelines for Eligible Applications:
• must be C and C++ applications;
• must have been compiled with the same compiler and OS version on both the Originating
Platform and the Target Platform;
• must have been compiled using a supported Oracle Solaris Studio compiler on a
supported OS release. 
```
