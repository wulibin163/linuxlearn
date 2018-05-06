# README

## 编译问题

1. 原始下载地址：http://oldlinux.org/Linux.old/kernel/0.1x/linux-0.11-060618-gcc4.tar.gz

2. 报错 Error: unsupported instruction `mov'

原因是在x64架构的机器上编译，需要给编译器指定用32位，在所有Makefile的AS后面添加--32，CC后面加-m32, LD后面加-m elf_i386

3. 报 strcpy 等符号重定义

将 include/string.h 里边的 extern 全部改成 static

4. 报 invalidate_buffers 找不到

将 fs/buffer.c 里边 invalidate_buffers 前的 inline 去掉

5. 在 console.c 中清楚定义了 static unsigned char attr = 0x70,而在链接 console.o 时，却爆出 attr未定义。

用 nm 查看 console 确实发现没定义， 应该是被编译器优化掉了， 修改 Makefile 将 -O 删除

6. 报 sys/cdefs.h 找不到

apt-get install libc6-dev-i386

