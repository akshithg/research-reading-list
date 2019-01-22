# PT-Rand: Practical Mitigation of Data-only Attacks against Page Tables

- NDSS 2017
- [dblp](https://dblp.uni-trier.de/rec/html/conf/ndss/DaviGLS17)
- [youtube](https://www.youtube.com/watch?v=l-ou5LqOOy4)

## Summary

Current Kernel hardening solutions e.g. DEP to prevent code injection, CFI to prevent code-reuse exploits rely on the assumption that **kernel page tables cannot be manipulated** with data only attacks. Existing solutions require hardware trust anchors, costly hypervisors or inefficient integrity checks.

This paper proposes a data-only attack against page tables on a recent CFI hardened (using RAP) kernel and then proposes a defence called PT-Rand, which randomizes the location of the page table, and also ensuring the location of the page table is not leaked thereby preventing data-only attacks on page table.

Their evaluations show a overhead of .22% (SPEC).

Assumptions:

- There exists and kernel/driver memory corruption vulnerability.
- Attacker has full control of the user space
- User-mode pages are not accessible (SMAP/SMEP)
- W oxr X protection exists
- Code-reuse defences (CFI, CPI, RAP) exist
- DMA protection exists
- Safe initialization, no attack before kernel initialization
- A secure random number generator is available
- Side-Channels beyond scope

Goals:

- To randomize the location of the page table and prevent leakage of the random secret
- substitute pointers that reference page tables with physical addresses to obfuscate these references.

Design:

- in allocator functions for page table
    - move the initial page tables to a random address
    - always return physical addresses for any page table related memory allocation
- to allow benign kernel code to access the page tables
    - convert the physical address to a virtual address based on the randomization secret generated

### Good

- Breaks down a critical assumption.
- Performance is good.

### Bad

- physmap (kernel's 1:1 map) no longer available.

### What would you do next

### Questions

Explain RAP: RIP ROP?
