# Kernel Data Attack is a Realistic Security Threat


- [SecureComm 2015](https://link.springer.com/chapter/10.1007%2F978-3-319-28865-9_8)
- [dblp](https://dblp.uni-trier.de/rec/html/conf/ndss/VoglPKE14)

## Summary

By altering in-memory kernel data, attackers can manipulate the OS without injecting any code. This paper thoroughly investigate kernel data attacks and develop a new key logger called DLOGGER which only alters kernel data and leverages existing benign kernel code to build a covert channel, through which attackers can steal sensitive information. And propose a mechanism to detect a kernel data attack.

- 380,000 global function pointers and global variables
- the runtime behavior of kernel internal defense mechanisms rely on some global kernel data
- they provide a kernel data classification and by treating different types of data separately, they propose a defense that is effective in detecting kernel data attacks


Classifications:

- Kernel Global data vs local data: Use proc file system file, /proc/kallsyms to find symbol-to-virtual-memory-address mapping. Overwrite that memory are to change values.

- read-only data and read-write data: protecting kernel read-write data is more challenging, as the vast majority of these data are subject to change at runtime.

- function pointers and variables: do not consider hooking any function pointers (no code injection) and our focus is on variables only

Attacks:

- Bypass Linux Auditing: audit_n_rules is a globally defined variable. Set to 0.

- Bypassing AppArmour:  g_profile_mode and g_apparmor_audit. Set to "complain" profile mode and the "quiet" audit type.

- Bypass NULL Pointer Dereference Mitigation: mmap_min_addr, which specifies the minimum virtual address that a process is allowed to map. Set to 0.

Defense:

- Type 1: Read-only data.
- Type 2: Modifiable data that normally remains constant across different systems.
- Type 3: Modifiable data that normally does not change, but can differ from system to system.
- Type 4: Modifiable data that changes frequently.

1. set up multiple identical virtual machines
2. get all the variable symbols from /proc/kallsyms and put them into ListAll
3. List1, List2, List3, and List4 to represent the symbol lists for Type 1, Type 2, Type 3, and Type 4
4. List1: symbols are explicitly marked i "r" or "R"
5. List2: The RW list which are same on all VMs
6. Type 3 and Type 4: measure value from VM at multiple points during a span of multiple days. If no changes were identified, put it into List3; otherwise, put it into List4

Defense method:

- Type 1: Easy to defend (prior work: VM Introspection)
- Type 2: PeerPressure (MSR, hardware-based page-level protection)
- Type 3: Tripwire (notify on change)
- Type 4: No attacks detected.

### Good

### Bad

### What would you do next

### Questions

CFI, CPI timeline?
