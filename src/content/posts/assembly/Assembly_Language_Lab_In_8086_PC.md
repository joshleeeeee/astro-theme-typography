---
title: 《汇编语言》第4版.王爽 Lab 全集
categories:
  - 汇编
pubDate: 2023-08-22
---

# Assembly Language Lab In 8086PC

> 使用教材：《汇编语言》第 4 版 - 王爽
## 环境搭建

由于王爽的《汇编语言》是以 `Intel 8086` CPU为基础进行教学的，全书处于实模式（Real Mode）中进行讲解，在 Real Mode 下 CPU 以 16 位模式运行，可以访问 1MB 的物理内存，并且没有内存保护的机制，可以随意访问和修改其他程序的内存，这是相当的有利于我们学习~

而现代的操作系统，如 Windows10、Windows11 通常使用的是保护模式（Protected Mode）和长模式（Long Mode），这也就意味着我们想要运行书中的汇编代码，需要使用模拟器（DOSBox）去模拟早期的 DOS 操作系统环境。

下面进入正题，将介绍如何在现代的操作系统中搭建 8086CPU 的环境

1. 下载并安装 [DOSBox](https://www.dosbox.com/)
2. 下载 [DEBUG.COM](https://github.com/microsoft/MS-DOS/blob/master/v2.0/bin/DEBUG.COM) 文件并放入 `[Your Folder]` 内，注意`[Your Folder]` 指的是你自己的文件夹路径，请将此替换成你自己的路径，如 `D:\Debug` 。 *// 在MS-DOS中，扩展名为`.COM` 的文件通常是可执行的二进制文件，全称为"Command File"，即“命令文件”* 
3. 配置 DOSBox
	1. **打开配置文件**：打开 DOSBox 的安装目录，双击运行`DOSBox 0.74-3 Options.bat`，成功运行后会自动打开配置文件 `dosbox-0.74-3.conf`。若你使用的是 Mac OS ，则可以直接打开配置文件 `~/Library/Preferences/DOSBox 0.73 Preferences`，其余方法和 Windows 同理。
	2. **添加启动后自动执行的命令**：直接前往配置文件的底部，在`[autoexec]`下添加下面代码（记得改成自己的路径）

```
MOUNT C [Your Folder]
C:
DEBUG.com
```
最后保存文件然后退出。

做到这里，将DOSBox运行起来，不出意外的话会自动运行 `debug` 程序，可以输入 `r` 命令验证一下，效果如下，这样就大功告成啦~

![](/images/assembly/asm_lab_01.png)

## 实验1 查看CPU和内存，用机器指令和汇编指令编程

### (Register) 查看、改变CPU寄存器内容

> `r [register]`

查看所有的 8086 寄存器的内容 `r`：

![](/images/assembly/asm_lab_02.png)

改变寄存器的内容 `r [寄存器名称]`：

![](/images/assembly/asm_lab_03.png)

### (Dump) 查看内存

> `d [range]`

- `d [段地址:偏移地址]`
	- 查看内存 10000H 处的内容：`d 1000:0`
	- 查看内存 11451H 处的内容：`d 1145:1`
- `d [段地址:偏移地址] [长度]`
	- 查看 1000:0~1000:9 中的内容：`d 1000:0 9`
	- 仅查看内存单元 10000H 中的内容：`d 1000:0 0`

### (Enter) 改写内存内容

> `e address [list]`

- 将内存 1000:0~1000:9 单元中的内容分别写为1~9: `e 1000:0 0 1 2 3 4 5 6 7 8 9`
- 向内存 1000:10 处写入字符串"Hello, World"：`e 1000:10 "Hello, World"`

同理也可以在内存中写入机器码 `e 1000:0 b8 01 00 b9 02 00 01 c8`

| 机器码  | 对应的汇编指令 |
| ------- | -------------- |
| b80100 | `mov ax,0001`  |
| b90200  | `mov cx,0002`  |
| 01c8    | `add ax cx`    |

接下来我们可以用 `u` 命令进行反汇编d 200
### (Unassemble) 将内存中的机器指令翻译成汇编指令

> `u [range]`

`u 1000:0`:

![](/images/assembly/asm_lab_05.png)
### (Trace) 执行一条机器指令

> `t [=address] [number]`

在内存地址 1000:0 处执行并追溯两条指令：

![](/images/assembly/asm_lab_06.png)
### (Assemble) 以汇编指令的格式在内存中写入一条机器指令

> `a [address]`

从内存 1000:0 开始写入指令：

```
-a 1000:0
1000:0000 mov ax,1
1000:0003 mov bx,2
1000:0006 mov cx,3
```

## 实验2 用机器指令和汇编指令编程

### 实验任务 1

> 使用 Debug，将下面的程序段写入内存，逐条执行，根据指令执行后的实际运行情况填空

---

``` asm
mov ax,ffff
mov ds,ax

mov ax,2200
mov ss,ax

mov sp,0100

mov ax,[0]            ;ax=C0EA
add ax,[2]            ;ax=C0FC
mov bx,[4]            ;bx=30F0
add bx,[6]            ;bx=6021

push ax               ;sp=00FE; 修改的内存单元的地址是 2200:00FE 内容为 C0FC
push bx               ;sp=00FC; 修改的内存单元的地址是 2200:00FC 内容为 6021
pop ax                ;sp=00FE; ax=6021   
pop bx                ;sp=0100; bx=C0FC

push [4]              ;sp=00FE; 修改的内存单元的地址是 2200:00FE 内容为 30F0
push [6]              ;sp=00FC; 修改的内存单元的地址是 2200:00FC 内容为 2F31
```

### 实验任务 2

> 观察下图中的实验过程，然后分析：为什么2000:0~2000:f中的内容会发生改变？
> 可能要再做些实验才能发现其中的规律。如果你在这里就正确回答了这个问题，那么要恭喜你，因为你有很好的悟性。大多数的学习者对这个问题还是比较迷惑的，不过不要紧，因为随着课程的进行，这个问题的答案将逐渐变得显而易见。

---



![](/images/assembly/asm_lab_07.png)

2023-8-8 20:51:28：确确实实，执行了 `MOV SS,AX` 后 `MOV SP 10` 也会自动执行，栈内存会被填充一些数据，通过分析发现被填充的是 `IP`, `DS` 和 `ES`，但具体用处还有待研究

![](/images/assembly/asm_lab_08.png)

## 实验3 编程、编译、连接、跟踪

### 实验任务1

> 将下面的程序保存为 `t1.asm` 文件，将其生成可执行文件 `t1.exe`
>
> ``` asm
> assume cs:codesg
> 
> codesg segment
> 
> 	mov ax,2000H
> 	mov ss,ax
> 	mov sp,0
> 	add sp,10
> 	pop ax
> 	pop bx
> 	push ax
> 	push bx
> 	pop ax
> 	pop bx
> 
> 	mov ax,4c00H
> 	int 21H
> 
> codesg ends
> 
> end
> ```

---

由于我们使用的是 `DOSBox`，需要下载[编译器(masm)](https://github.com/microsoft/MS-DOS/blob/master/v2.0/bin/MASM.EXE)，[连接器(link)](https://github.com/microsoft/MS-DOS/blob/master/v2.0/bin/LINK.EXE)和[编辑器(edit)](http://www.thealmightyguru.com/Wiki/index.php?title=MS-DOS_Editor)，并且将其放到你所挂载的目录`[Your Folder]`，如 `D:\debug`

出于个人习惯问题，我比较喜欢用一些流行的编辑器，比如 `Sublime Text`。我们在 `[Your Folder]` 中新建个文件，并改名为 `t1.asm`，然后开始写代码。

写完代码之后，我们重启 DOSBox 以重新挂载目录，然后开始编译 `masm c:\t1;` 得到`T1.OBJ`，最后进行连接 `link t1;` 得到可执行文件 `T1.EXE`

### 实验任务2

> 用Debug跟踪 `t1.exe` 的执行过程，写出每一步执行后，相关寄存器的内容和栈顶的内容

---

**答：**

用 Debug 运行 t1.exe: `debug T1.EXE`

---

![](/images/assembly/asm_lab_09.png)

---

![](/images/assembly/asm_lab_10.png)

---

![](/images/assembly/asm_lab_19.png)

---

![](/images/assembly/asm_lab_11.png)

---

![](/images/assembly/asm_lab_12.png)

---

![](/images/assembly/asm_lab_13.png)

---

![](/images/assembly/asm_lab_14.png)

---

![](/images/assembly/asm_lab_15.png)

---

![](/images/assembly/asm_lab_16.png)

---

![](/images/assembly/asm_lab_17.png)

### 实验任务3

>PSP的头两个字节是`CD 20`，用 Debug 加载 `t1.exe`，查看 PSP 的内容

---

**答：**

通过 `r` 命令我们可知 `CS` 为 `04AD`，那么PSP的地址则为 `04ADH-10H=049D`，查看其内存，发现开头两个字节确实如此

![](/images/assembly/asm_lab_18.png)

可以看到 PSP 的首个指令为 `INT 20` ，是一个软中断（Software interrupt）指令，用于向 DOS 操作系统发出终止程序的请求。

## 实验4 `[bx]`和`loop`的使用

### 实验任务1 

> 编程，向内存 `0:200` ~ `0:23F` 依次传递数据 0~63(3FH)

---

**答：**

``` asm
assume cs:codesg

codesg segment

	mov ax,0
	mov ds,ax
	mov bx,200h
	mov cx,40h
s:  mov [bx],ax
	inc bx
	inc ax
	loop s
	
	mov ax,4c00h
	int 21h

codesg ends

end
```

### 实验任务2

> 编程，向内存 `0:200` ~ `0:23F` 依次传递数据 0~63(3FH)，程序中只能使用 9 条指令，9 条指令中包括 `mov ax,4c00h` 和 `int 21h`

---

**答：**

``` asm
; Acknowledgement: chan_honman 
assume cs:codesg

codesg segment

	mov ax,20h
	mov ds,ax
	mov bx,0
	mov cx,40h
s:  mov [bx],bx
	inc bx
	loop s
	
	mov ax,4c00h
	int 21h

codesg ends

end
```

### 实验任务3

>下面的程序的功能是将 `mov ax,4c00h`  之前的指令复制到内存 0:200 处，补全程序。上机调试，跟踪运行结果。
>
>``` asm
> assume cs:code
>
> code segment
>
>	mov ax,____
>	mov ds,ax
>	mov ax,0020h
>	mov es,ax
>	mov bx,0
>	mov cx,____
> s:  mov al,[bx]
>	mov es:[bx],al
>	inc bx
>	loop s
>	mov ax,4c00h
>	int 21h
>
> code ends
>
> end
>```
>
>提示：
>1. 复制的是什么？从哪里到哪里？
>2. 复制的是什么？有多少个字节？你如何知道要复制的字节的数量？

---

**答：**

复制的是可执行文件的机器指令，从 `cs` 复制到内存 20:0 处，故第一个空填入 **cs**

通过 `u` 命令对程序进行反汇编，可得知每条指令对应的机器码和其所占用的字节数
- `inc register` 这种类型的指令占用 1 Byte
- `mov register,register` 和 `loop` 类型的指令占用 2 Byte，如 `MOV DS,AX`，对应的机器码为`8ED8`
- `mov register,value` 这种类型的指令占用 3 Byte

``` asm
assume cs:code

code segment

	mov ax,cs          ; 2B
	mov ds,ax          ; 2B
	mov ax,0020h       ; 3B
	mov es,ax          ; 2B
	mov bx,0           ; 3B
	mov cx,23          ; 3B
s:  mov al,[bx]        ; 2B
	mov es:[bx],al     ; 2B
	inc bx             ; 1B
	loop s             ; 2B
	mov ax,4c00h
	int 21h

code ends

end
```

计算逐个指令后，可得出 `mov ax,4c00h` 之前的指令共占 **22** 字节，又因为每次 loop 只会复制一个字节，则需要循环 23 次，故第二个空填入 **23**

## 实验 5 编写、调试具有多个段的程序



### 实验任务 1

>  将下面的程序编译、连接，用 Debug 加载、跟踪，然后回答问题。
>
> ``` asm
> assume cs:code,ds:data,ss:stack
> 
> data segment
> 	dw 0123h,0456h,0789h,0abch,0defh,0fedh,0cbah,0987h
> data ends
> 
> stack segment
> 	dw 0,0,0,0,0,0,0,0
> stack ends
> 
> code segment
> 
> start: mov ax,stack
>        mov ss,ax
>        mov sp,16
>        
>        mov ax,data
>        mov ds,ax
>        
>        push ds:[0]
>        push ds:[2]
>        pop ds:[2]
>        pop ds:[0]
>        
>        mov ax,4c00h
>        int 21h
> 
> code ends
> end start
> ```
>
> 1. CPU执行程序，程序返回前，data 段中的数据为多少？
> 2. CPU 执行程序，程序返回前，`cs=_____`、`ss=_____`、`ds=_____`。
> 3. 设程序加载后，code 段的段地址为 X，则 data 段的段地址为 `_____`，stack 段的段地址为 `_____`。

---

**答：**

1. `0123h,0456h,0789h,0abch,0defh,0fedh,0cbah,0987h`
2. `CS=04AF`, `SS=04AE`,`DS=04AD`
3. `X-2`, `X-1`

### 实验任务 2

> 将下面的程序编译、连接，用 Debug 加载、跟踪，然后回答问题。
>
> ``` asm
> assume cs:code,ds:data,ss:stack
> 
> data segment
> 	dw 0123h,0456h
> data ends
> 
> stack segment
> 	dw 0,0
> stack ends
> 
> code segment
> 
> start: mov ax,stack
>     mov ss,ax
>     mov sp,16
> 
>     mov ax,data
>     mov ds,ax
> 
>     push ds:[0]
>     push ds:[2]
>     pop ds:[2]
>     pop ds:[0]
> 
>     mov ax,4c00h
>     int 21h
> 
> code ends
> end start
> ```
>
> 1. CPU执行程序，程序返回前，data 段中的数据为多少？
> 2. CPU 执行程序，程序返回前，`cs=_____`、`ss=_____`、`ds=_____`。
> 3. 设程序加载后，code 段的段地址为 X，则 data 段的段地址为 `_____`，stack 段的段地址为 `_____`。
> 4. 对于如下定义的段：
>
> ```
> name segement
> ...
> name ends
> ```
>
> ​		如果段中的数据占 N 个字节，则程序加载后，该段实际占有的空间为 `_____`。

---

**答：**

1. `23 01 56 04`
2. `CS=04AF`, `SS=04AE`, `DS=04AD`
3. `X-2`, `X-1`
4. $[(N+15)/16]*16$

### 实验任务 3

>  将下面的程序编译、连接，用 Debug 加载、跟踪，然后回答问题。
>
> ``` asm
> assume cs:code,ds:data,ss:stack
> 
> code segment
> start: 
> 	mov ax,stack
>     mov ss,ax
>     mov sp,16
> 
>     mov ax,data
>     mov ds,ax
> 
>     push ds:[0]
>     push ds:[2]
>     pop ds:[2]
>     pop ds:[0]
> 
> 	mov ax,4c00h
> 	int 21h
> code ends
> 
> data segment
> 	dw 0123h,0456h
> data ends
> 
> stack segment
> 	dw 0,0
> stack ends
> 
> end start
> ```
>
> 1. CPU执行程序，程序返回前，data 段中的数据为多少？
> 2. CPU 执行程序，程序返回前，`cs=_____`、`ss=_____`、`ds=_____`。
> 3. 设程序加载后，code 段的段地址为 X，则 data 段的段地址为 `_____`，stack 段的段地址为 `_____`。

---

**答：**

1. 仍不变，为：`21 01 56 04 ...`
2. `CS=04AD`, `SS=04B1`,`DS=04B0`
3. `X+3`, `X+4`

### 实验任务 4

> 如果将实验任务 1、2 和 3 题中的最后一条伪指令“end start”改为“end”（也就是说不指明程序的入口），则哪个程序仍然可以正常执行？请说明原因

---

**答：**

第三题的可以正常执行，因为它的代码段在前面，而前两题的程序都是数据段放在前面，没有标记程序的入口程序则会将 IP 指向到程序的最上方，也就是数据段，从而将数据段的机器码错误地当做指令去执行，那显然是错误的。

### 实验任务 5

> 程序如下，编写 code 段中的代码，将 a 段和 b 段中的数据依次相加到 c 段中。
>
> ``` asm
> assume cs:code
> a segment
> 	db 1,2,3,4,5,6,7,8
> a ends
> b segment
> 	db 1,2,3,4,5,6,7,8
> b ends
> c segment
> 	db 0,0,0,0,0,0,0,0
> c ends
> code segment
> start:
> 	?
> code ends
> end start
> ```

---

**答：**

首先能想到的最简单粗暴的办法就是不断的更换 DS 去计算 a 段和 b 段的数据，代码如下，显得非常冗余

``` asm
assume cs:code
a segment
	db 1,2,3,4,5,6,7,8
a ends
b segment
	db 1,2,3,4,5,6,7,8
b ends
c segment
	db 0,0,0,0,0,0,0,0
c ends
code segment
start:
	mov cx,8
	mov bx,0

s:  mov dx,0

    mov ax,a
    mov ds,ax
    add dx,[bx]
    
    mov ax,b
    mov ds,ax
    add dx,[bx]
    
    mov ax,c
    mov ds,ax
    mov [bx],dx
    
    inc bx
	loop s

	mov ax,4c00h
	int 21h
code ends
end start
```

但通过前几个实验，我们可以知道 a 段和、b 段和 c 段都是可以通过计算而得出来的，如果a段的地址为`X:0`, 那么 b 段的地址则为 `X:10`, c 段的地址则为 `X:20`，那么我们就可以利用这个特性去简化代码了，如下：

``` asm
assume cs:code

a segment
    db 1,2,3,4,5,6,7,8
a ends

b segment
    db 1,2,3,4,5,6,7,8
b ends

c segment
    db 0,0,0,0,0,0,0,0
c ends

code segment
start:
    mov ax,a
    mov ds,ax
    mov cx,8
    mov bx,0
    mov si,10h
    mov di,20h
s:  
    mov ax,[bx]
    add ax,[bx+si]
    mov [bx+di],ax
    add bx,2
    loop s

    mov ax,4c00h
    int 21h
code ends

end start
```

### 实验任务 6

> 程序如下，编写 code 段中的代码，用 push 指令将 a 段中的前 8 个字型数据，逆序存储到 b 段中。
>
> ``` asm
> assume cs:code
> a segment
> 	dw 1,2,3,4,5,6,7,8,9,0ah,0bh,0ch,0dh,0eh,0fh,0ffh
> a ends
> b segment
> 	dw 0,0,0,0,0,0,0,0
> b ends
> code segment
> 	?
> code ends
> end start
> ```

---

**答：**

根据题目的要求可知，我们将 b 段设为栈，长度为 16 字节，push 的时候刚好就可以将 a 段的前 8 个数据逆序，代码如下：

``` asm
assume cs:code
a segment
    dw 1,2,3,4,5,6,7,8,9,0ah,0bh,0ch,0dh,0eh,0fh,0ffh
a ends
b segment
    dw 0,0,0,0,0,0,0,0
b ends
code segment
start:
    mov ax,b
    mov ss,ax
    mov sp,16
    mov cx,8
    mov ax,a
    mov ds,ax
    mov bx,0
s:  push [bx]
    add bx,2
    loop s

    mov ax,4c00h
    int 21h
code ends
end start
```



## 实验 6 实践课程中的程序

### 实验任务 1

> 将课程中所有讲解过的程序上机调试，用 Debug 跟踪其执行过程，并在过程中进一步理解所讲内容。

### 实验任务 2

> 编程，完成问题7.9中的程序。
>
> 问题 7.9：将 datasg 段中每个单词的前 4 个字母改为大写字母
>
> ``` asm
> assume cs:codesg,ss:stacksg,ds:datasg
> 
> stacksg segment
>   dw 0,0,0,0,0,0,0,0
> stacksg ends
> 
> datasg segment
>   db '1. display      '
>   db '2. brows        '
>   db '3. replace      '
>   db '4. modify       '
> datasg ends
> 
> codesg segment
>   start: 
> codesg ends
> 
> end start
> ```

---

**答：**

``` asm
assume cs:codesg,ss:stacksg,ds:datasg

stacksg segment
  dw 0,0,0,0,0,0,0,0
stacksg ends

datasg segment
  db '1. display      '
  db '2. brows        '
  db '3. replace      '
  db '4. modify       '
datasg ends

stacksg segment
	dw 0,0,0,0,0,0,0,0
stacksg ends

codesg segment

  start: mov ax,stacksg
  	     mov ss,ax
  	     mov sp,16
  		 mov ax,datasg
  	     mov ds,ax
  	     mov cx,4
  	     mov bx,0
  	  s0:push cx
  	     mov cx,4
  	     mov si,0
      s: mov al,[bx+si+3]
         and al,11011111B
         mov [bx+si+3],al
         inc si
         loop s
         
         add bx,16
         pop cx
         loop s0
         
         mov ax,4c00h
         int 21h
         
codesg ends

end start
```

## 实验 7 寻址方式在结构化数据访问中的应用

>Power idea 公司从 1975 年成立一直到 1995 年的基本情况如下
>
>| 年份 | 收入(千美元) | 雇员(人) | 人均收入(千美元) |
>| ---- | ------------ | -------- | ---------------- |
>| 1975 | 16           | 3        | ?                |
>| 1976 | 22           | 7        | ?                |
>| 1977 | 382          | 9        | ?                |
>| 1978 | 1356         | 13       | ?                |
>| 1979 | 2390         | 28       | ?                |
>| 1980 | 8000         | 38       | ?                |
>| ...  | ...          | ...      | ...              |
>| 1995 | 5937000      | 17800    | ?                |
>
>``` asm
> data segment
>    db '1975, 1976, 1977, 1978, 1979, 1980, 1981, 1982', '1983'
>    db '1984, 1985, 1986, 1987, 1988, 1989, 1990, 1991, 1992'
>    db 1993, 1994, 1995!
>    ;以上是表示21年的21个字符串
>    
>    dd 16,22,382,1356,2390, 8000, 16000,24486,50065,97479,140417,197514
>    dd 345980, 590827, 803530,1183000,1843000,2759000, 3753000, 4649000,5937000
>    ;以上是表示21年公司总收入的21个 dword 型数据
>    
>    dw 3,7,9,13,28, 38,130,220,476, 778, 1001, 1442,2258,2793, 4037, 5635, 8226
>    dw 11542, 14430,15257,17800
>    ;以上是表示21年公司雇员人数的21个word型数据
> data ends
> table segment
>	db 21 dup ('year summ ne ??)
> table ends
>```

## 实验 10 编写子程序

> 在指定的位置，用指定的颜色，显示一个用 0 结束的字符串。
>
> 参数：(dh)=行号，(dl)=列号
>
> ​			(cl)=颜色，ds:si 指向字符串的首地址。
>
> ``` asm
> assume cs:code
> data segment
>     db 'Welcome to masm!',0
> data ends
> 
> code segment
> 
> start:  mov dh,8
>         mov dl,3
>         mov cl,2
>         mov ax,data
>         mov ds,ax
>         mov si,0
>         call show_str
> 
>         mov ax,4c00h
>         int 21h
> show_str:
>         mov ds,b800h
> 
> 
> code ends
> end start
