## Introduction of Virtual Memory <br>虚拟内存的引入

**虚拟内存 (virtual memory)** 使用主存 (main memory) 和辅助存储器 (secondary memory) 的结合来扩展可用内存空间，将主存作为辅助存储器的高速缓存，从而使得**规模比实际物理内存容量更大**的程序能够运行。

由于主存容量有限，虚拟内存通过将不常用的数据和程序代码临时存储在辅助存储器（如硬盘）上，实现了对更大内存空间的访问。这种机制使得程序可以使用比实际物理内存更大的地址空间，从而提高了系统的灵活性和效率。

## Structure of Virtual Address Space <br>虚拟地址空间的结构

### Translation Lookaside Buffer (TLB) <br>地址转换旁路缓存

**地址转换旁路缓存 (Translation Lookaside Buffer, TLB)** 是一种特殊的高速缓存，用于存储最近使用的**虚拟地址到物理地址的映射**。TLB 的主要作用是加速地址转换过程，减少访问页表的次数，从而提高内存访问速度。

与其他缓存表类似，TLB 也有直接映射 (direct mapped)、全相联 (fully associative) 和组相联 (set associative) 等不同的组织方式。TLB 的高命中率对于系统性能至关重要，因为每次 TLB 未命中都需要访问较慢的页表，从而增加了内存访问时间。