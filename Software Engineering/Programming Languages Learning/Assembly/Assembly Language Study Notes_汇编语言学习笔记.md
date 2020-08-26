# Index

|[x86处理器架构](#x86处理器架构)|
|---|
|[32位x86处理器架构](#32位x86处理器架构)|
| x86-64处理器架构 |
| --- |
| 汇编语言基础 |
| --- |
| 常用汇编器 |
汇编语言常量	4
汇编语言保留字/关键字	4
标识符identifier	4
伪指令directive	4
指令	4
列表文件listing file	4
数据类型和数据定义	4
数据操作相关运算符和指令	3
操作数类型	4
MOV、MOVZX、MOVSX指令	4
LAHF、SAHF指令	4
XCHG指令	4
加减运算和相关指令	4
OFFSET运算符	4
ALIGH伪指令	4
PTR运算符	4
TYPE和SIZEOF运算符	4
LENGTHOF运算符	4
LABEL伪指令	4
TYPEDEF运算符	4
汇编语言条件判断	4
布尔和比较指令	5
检查奇偶标志	5
置位和清除单个CPU标志	5
JMP指令	5
条件跳转指令	5
LOOP相关指令	5
32位条件控制流伪指令	5
汇编语言整数运算	4
逻辑移位和算术移位	5
MUL指令	5
IMUL指令	5
DIV指令	5
IDIV指令	5
符号扩展指令	5
ADC和SBB指令	5
汇编语言ASCII和非压缩十进制运算	5
压缩十进制运算	5
汇编语言过程	4
PUSH和POP及相关指令	5
CALL和RET指令	5
USES运算符	5
汇编语言高级过程	4
调用规范	5
LEA指令	5
ENTER和LEAVE指令	5
LOCAL伪指令	5
INVOKE伪指令	5
ADDR运算符	5
PROC和ENDP伪指令	5
PROTO伪指令	5
EXTERN伪指令	5
Java虚拟机JVM工作原理	5
汇编语言字符串和数组	4
字符串基本指令	5
汇编语言结构和宏	4
结构体	5
联合union	5
宏过程简述	5
条件汇编伪指令简述	5
宏汇编运算符简介	5
宏函数	5
重复语句伪指令	5
浮点数处理与指令编码	4
FPU浮点数计算单元简介	4
浮点数异常	4
浮点数指令集	4
FINIT初始化	4
FLD加载浮点数值	4
FST，FSTP保存浮点数值	4
FCHS和FABS	4
FADD、FADDP、FIADD	4
FSUB、FSUBP、FISUB	4
FMUL、FMULP、FIMUL	5
FDIV、FDIVP、FIDIV	5
FCOM、FCOMP、FCOMPP	5
FWAIT指令（WAIT）	5
其他FPU指令	5
高级语言接口	5
.MODEL伪指令	5
__asm伪指令	6
部分汇编器特殊语法积累	6
MASM	6
Visual Studio常用功能积累	7
查看OBJ文件中所有过程名	7
查看编译器生成的汇编语言代码	7

# x86处理器架构
## 32位x86处理器架构
1）操作模式：

- 保护模式protected mode——一般的支持虚拟内存的模式
- 虚拟8086模式Virtual-8086——8086虚拟机，仅1MB内存，但可以创建多个
- 实地址模式Real-Address——MS-DOS模式，直接寻址，仅1MB内存和单程序
- 系统管理模式System Management——仅由操作系统和机器开发使用

2）地址空间：

最大4GB，从 P6 处理器开始，一种被称为扩展物理寻址 (extended physical addressing) 的技术使得可以被寻址的物理内存空间增加到 64GB

3）基本程序执行寄存器basic program execution registers

- 8个32位通用寄存器：
  - EAX：扩展累加器extended accumulator，乘除指令默认使用。也用于子程序存放返回值。
  - EBX：
  - ECX：CPU 默认使用 ECX 为循环计数器
  - EDX：
  - EBP：扩展帧指针extended frame pointer，用于引用堆栈数据，指向当前调用堆栈帧首地址。极少作算术和传输。
  - ESP：扩展堆栈指针extended stack pointer，用于寻址堆栈数据，指向调用堆栈的顶部地址。极少作算术和传输。
  - ESI：扩展源变址extended source index，用于高速存储器传输指令，也常常用作基址-偏移量寻址中存放指针数据。
  - EDI：扩展目的变址extended destination index，用于高速存储器传输指令

注：EAX的低16位叫AX，AX的高低8位分别叫AH和AL，以此类推（仅限ABCD这4个通用寄存器可以拆开使用）。

- 6个16位段寄存器：
  - CS
  - SS
  - DS
  - ES
  - FS
  - GS

注：实地址模式中，16 位段寄存器表示的是预先分配的内存区域的基址，这个内存区域称为段。保护模式中，段寄存器中存放的是段描述符表指针。

- 1个指令指针寄存器（EIP）：包含下一条将要执行指令的地址
- 1个处理器状态标志寄存器（EFLAGS）：
  - 控制标志位——控制标志位控制 CPU 的操作。
  - 状态标志位——
  - 进位标志位CF——无符号算术运算结果太大或为负时，设置该标志位
  - 溢出标志位OF——有符号算术运算结果太大或太小时，设置该标志
  - 符号标志位SF——算术或逻辑操作产生负结果时，设置该标志位。
  - 零标志位ZF——算术或逻辑操作产生的结果为零时，设置该标志位。
  - 辅助进位标志位AC——算术操作在 8 位操作数中产生了位 3 向位 4 的进位
  - 奇偶校验标志位PF——结果的最低有效字节包含偶数个 1 时设置，否则清除标志
- MMX寄存器：8 个 64 位 MMX 寄存器支持称为 SIMD的特殊指令
- XMM寄存器：8 个 128 位 XMM 寄存器，它们被用于 SIMD 流扩展指令集
- 浮点单元FPU, floating-point unit：执行高速浮点算术运算。FPU 中有 8 个80位浮点数据寄存器，ST(0)~ST(7)。还有48位指令指针寄存器，48位数据指针寄存器，16位标识寄存器，16位控制寄存器，16位状态寄存器，操作码寄存器。
