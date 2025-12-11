## Cache Management <br>缓存管理

### Cache mapping <br>缓存映射

缓存映射是指将主存地址映射到缓存中的过程，解决**如何在缓存中定位数据**的问题。

#### Direct-mapped cache <br>直接映射缓存

直接映射缓存是一种简单的缓存映射方式，其中每个主存块只能映射到缓存中的一个特定位置。主存地址被划分为三个部分：**标签 (tag)**、**索引 (index)** 和 **块内偏移 (block offset)**。

