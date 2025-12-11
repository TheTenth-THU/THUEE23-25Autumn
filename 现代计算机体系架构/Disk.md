## Magnetic Disk <br>磁盘

**磁盘 (magnetic disk)**，通常也称**机械硬盘 (hard disk drive, HDD)**，是一种常见的辅助存储器，广泛用于存储操作系统、应用程序和用户数据。磁盘通过磁性介质来存储数据，具有大容量和相对较低的成本优势。

### Disk structure <br>磁盘结构

磁盘通常由多个圆形的**盘片 (platter)**，每个盘片的一面或两面覆盖有磁性材料，用于存储数据。
+ 盘片上以同心圆形式排列的数据存储区域称为**磁道 (track)**，每一面通常有 10,000 到 50,000 个磁道。
+ 每个磁道进一步划分为 100 至 500 个**扇区 (sector)**，扇区是磁盘上**数据存储的基本单位**，通常每个扇区大小为 512 B。

数据通过**读写磁头 (read/write head)** 进行读写操作，磁头悬浮在盘片表面上方，通过机械臂移动到指定的磁道位置进行数据访问。

磁盘的访存时间通常由以下几个参数决定：
+ **寻道时间 (seek time)**：磁头移动到目标磁道所需的时间，通常在 3 ms 到 13 ms 范围内。由于**存储访问的空间局部性**，实际访存的平均寻道时间往往仅为标称 (advertised) 平均寻道时间的 25\% 到 33\%；
+ **旋转延迟 (rotational latency)**：等待目标扇区旋转到磁头下方所需的时间，为 $\cfrac{1}{2} \times \cfrac{1}{\text{RPM}}$；
+ **传输时间 (transfer time)**：将一个数据块（一个或多个扇区）从磁头下方传输到磁盘控制器缓存所需的时间，取决于磁盘的传输速率。
+ **控制器开销 (controller overhead)**：磁盘控制器处理 I/O 请求所需的时间，通常小于 0.2 ms。

> [!example] 磁盘访存时间计算示例
> 对于转速为 10,000 rpm 的磁盘，平均寻道时间为 6 ms，传输速率为 50 MB/s，控制器开销为 0.2 ms，读取或写入 512 B 扇区的平均时间为
> $$
> \begin{align}
> \text{Average disk access} &= \text{Average seek time} + \text{Average rotational latency} + \text{Transfer time} + \text{Controller overhead} \\
> &= 6 \rmu{ms} + \dfrac{1}{2} \times \dfrac{60 \rmu{s}}{10,000} + \dfrac{512 \rmu{B}}{50 \times 10^{6} \rmu{B/s}} + 0.2 \rmu{ms} \\
> &= 6 \rmu{ms} + 3 \rmu{ms} + 0.01024 \rmu{ms} + 0.2 \rmu{ms} \approx 9.21 \rmu{ms}
> \end{align}
> $$
> 若实际测得的平均寻道时间为标称的 25\%，则平均访存时间即约为 4.71 ms。


