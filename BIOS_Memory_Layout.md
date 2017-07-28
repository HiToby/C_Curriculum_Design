#BIOS_Memory_Layout
DOS操作系统运行在实模式下，在实模式下的寻址范围只有1MB。

DOS系统和程序适用16位“断基址：偏移量”格式，只能使用低端的640KB，这就是有名的640KB限制。

其中最低端的1KB,即00000H~003FFH存放的是中断矢量表；

接下来是256B的BIOS数据区；

DOS及应用程序使用00500H~9FFFFH。这在开始使用DOS的20世纪80年代是完全能够满足要求的，因为当时PC上安装的物理内存容量也是640KB，甚至更少。

系统硬件使用的内存位于地址区域的高端，范围是A0000H~FFFFFH，共384KB。其中有用于显示的视频缓冲区和BIOS程序空间，例如显卡，网卡和主板BIOS。

地址FFFF0H在PC中有特别的用途。系统在启动时，CS=F000H，IP=FFF0H，即从地址FFFF0H处开始执行，这个区域属于系统BIOS。（F000：FFF0）=EA5BE000F0（是JMP F000：E05B指令的十六进制表示），它立即跳转到BIOS的初始化程序，开始系统的启动过程。

<img src="Pictures\BIOS_Memory_Layout.jpg" style="zoom:80%" />