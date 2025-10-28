## Introduction <br>引入

### Instruction-level _v.s._ Machine-level Parallelism <br>指令级并行与机器级并行

#### Instruction-level Parallelism (ILP) <br>指令级并行

**指令级并行 (ILP)** 针对**程序**而言，是衡量处理器**可能同时执行**程序中指令平均数量的一项指标。ILP 反映了程序中**指令之间的独立性**和并行执行的潜力。ILP 的高低取决于程序的结构和编译器的优化能力，通常受限于**数据依赖**与**控制依赖**。

#### Machine-level Parallelism (MLP) <br>机器级并行

**机器级并行 (MLP)** 针对**处理器**而言，是衡量处理器**实际同时执行**指令平均数量的一项指标。MLP 反映了处理器**对程序 ILP 的利用能力**。MLP 的高低取决于处理器的架构设计、流水线深度、缓存层次结构以及多核处理能力。

### Instruction Issue & Completion Policies<br>指令发射与指令完成

指令开始执行的时刻称为**指令发射 (instruction issue)**，指令完成执行的时刻称为**指令完成 (instruction completion)**。指令发射与完成的策略影响处理器的并行度和性能，具体地：
+ 指令的发射影响**指令预取 (instruction lookahead) 能力**，即处理器能够获取、解码并发射超越当前执行点的指令，以尝试寻找更多可发射指令的能力；
+ 指令的完成影响**处理器前瞻 (processor lookahead) 能力**，即处理器能够检查超越当前执行点的已发射指令，以尝试寻找更多可完成指令的能力。

#### In-order Issue with In-order Completion <br>顺序发射顺序完成

最简单的策略是按照程序的确切顺序发出指令，并按照取指顺序（即程序顺序）完成指令，这称为**顺序发射、顺序完成 (in-order issue with in-order completion, IOI-IOC)**。

考虑如下指令序列：
```
I1 – needs two execute cycles (a multiply)  
I2  
I3
I4 – needs the same function unit as I3
I5 – needs data value produced by I4
I6 – needs the same function unit as I5
```
^557724

假定处理器为 IFID—EX—WB 三级结构，每周期可以取指、译码和发射 2 条指令，同时可以写回 2 条指令。按照 IOI-IOC 策略，指令的执行过程如下：

![[IOI-IOC.png|IOI-IOC]]

#### In-order Issue with Out-of-order Completion <br>顺序发射乱序完成

为了提升处理器的前瞻能力，可以允许指令按照程序顺序发射，但允许指令乱序完成，这称为**顺序发射、乱序完成 (in-order issue with out-of-order completion, IOI-OOC)**。

采用乱序完成机制时，后续指令可以先于前序指令执行完毕，由此**提升长延迟操作（如除法运算）的性能表现**。使用乱序完成时，若出现资源冲突（例如功能单元占用）或待发射指令所需数据尚未计算完成，指令发射仍将暂停。

考虑[[#^557724|上述指令序列]]，采用 IOI-OOC 策略，指令的执行过程如下：

![[IOI-OOC.png|IOI-OOC]]

当引入乱序完成机制后，处理器需要额外处理一类数据冒险，即**输出依赖 (output dependency)**，典型例子是**写前写 (write-before-write)**。假定
```
I1 - writes to R3
I2 - writes to R3
I5 - reads R3
```
如果 `I2` 在 `I1` 之前完成，则 `I5` 可能读到错误的 `R3` 值。为避免这种情况，处理器需要确保**后续指令的写回不会覆盖前序指令的结果**。

#### Out-of-order Issue with Out-of-order Completion <br>乱序发射乱序完成

采用顺序发射时，处理器一旦遇到已解码指令存在资源冲突或与已发射但未完成的指令存在数据依赖，便会**停止解码**指令。即使后续更多指令可能不存在冲突因而可被发射，处理器也无法查看超越冲突指令之后的内容。

为了进一步提升处理器的指令预取能力，可以在解码阶段与执行阶段之间插入**缓冲区 (buffer)** 存储暂时冲突指令之后的指令，并标记缓冲区中不存在资源冲突或数据依赖的指令，被标记的指令随后可不考虑其程序顺序而从缓冲区中发射，这称为**乱序发射、乱序完成 (out-of-order issue with out-of-order completion, OOI-OOC)**。

采用 OOI-OOC 策略时，处理器可以**更灵活地调度指令执行**，以最大化资源利用率和并行度；但同时，处理器需要复杂的硬件机制来跟踪指令的状态、管理数据依赖，并确保程序语义的正确性。

考虑[[#^557724|上述指令序列]]，采用 OOI-OOC 策略，指令的执行过程如下：

![[OOI-OOC.png|OOI-OOC]]

采用乱序发射机制时，处理器需要额外处理一类数据冒险，即**反向依赖 (antidependency)**，典型例子是**读前写 (write-before-read)**。假定
```
I1 - Uses R3 to compute a value and writes to R3
I2 - Reads R3
I3 - Writes to R3
```
如果 `I3` 在 `I1` 之前完成，则 `I2` 可能读到错误的 `R3` 值。为避免这种情况，处理器需要确保**后续指令的写回不会覆盖前序指令的值**。

> [!note] 反向依赖与真实依赖
> **反向依赖**约束与**真实依赖 (true dependency)** 相似，但方向相反。
> + 真实依赖的冒险是因为后一条指令使用了前一条指令（尚未）产生的值，即**写前读 (read-before-write)**；
> + 反向依赖的冒险是因为后一条指令覆盖了前一条指令（尚未）使用的值，即**读前写 (write-before-read)**。

## Very Long Instruction Word (VLIW) Architecture <br>超长指令字体系结构

### Basic Concept <br>基本概念

**超长指令字 (Very Long Instruction Word, VLIW)** 体系结构是一种处理器设计方法，通过将多条操作编码在单个超长指令字中，实现**高指令级并行性 (ILP)**。VLIW 处理器**依赖编译器**在编译时识别和调度可并行执行的指令，从而简化硬件设计，提升执行效率。

VLIW 打包在一个时钟周期内发射的指令组合称为**发射包 (issue packet)**，包内捆绑的指令类型的组合通常是有限的。

> [!example] VLIW MIPS 发射包示例
> 考虑一个 2 发射 VLIW MIPS 处理器，其发射包设定为
> ```tx
> | 64 bits ||
> | Slot 1        | Slot 2        |
> |:--------------|:--------------|
> | ALU 指令 (R)  | Load/Store 指令 (L) |
> | Branch 指令 (I) | Load/Store 指令 (L) |
> | Any | Nop |
> ```

这一简单的设定要求：
+ 寄存器堆有 4 个读端口和 2 个写端口，以支持包内指令的并行读写；
+ 内存地址计算拥有独立的 ALU 单元，以支持 Load/Store 指令的并行执行。

### Branch prediction <br>分支预测技术

在 VLIW 体系结构中，**分支预测 (branch prediction)** 技术尤为重要，因为错误的分支预测会导致整个发射包的指令被浪费。

分支预测包括两种主要方法：
+ **静态分支预测 (static branch prediction)**：基于固定规则进行预测，例如总是预测向前跳转不发生，向后跳转发生。
+ **动态分支预测 (dynamic branch prediction)**：利用历史信息和模式识别进行预测，例如使用分支历史表 (Branch History Table, BHT) 来记录分支的过去行为。
