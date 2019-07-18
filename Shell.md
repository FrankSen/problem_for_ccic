# 目录

* [软连接和硬链接的区别](#软链接和硬链接的区别)

## 软连接和硬链接的区别

- 软链接：
1. 创建软连接
```
➜  openproject ln -s /home/franksen/openproject/README-zh.md ./read
➜  openproject ll
总用量 44K
lrwxrwxrwx 1 franksen franksen   39 7月  18 15:24 read -> /home/franksen/openproject/README-zh.md
-rw-r--r-- 1 franksen franksen  40K 7月  18 14:19 README-zh.md

```

- 软链接删除源文件，链接无效
- 软链接如Windows环境中的快捷方式，由指向目标文件的路径构成 
- 软链接文件的inode与源文件不同
- 可以跨分区
- 软链接失效时，字体会出现红色
 
2. 创建硬链接

```
➜  openproject head -10 README-zh.md > cangls.md
➜  openproject ln ~/openproject/cangls.md ~/openproject/mycangls   
# 使用ls -i 查看文件的节点编号
➜  openproject ls -li，可见硬链接节点编号相同
总用量 52
281291 -rw-r--r-- 2 franksen franksen   842 7月  18 15:27 cangls
281291 -rw-r--r-- 2 franksen franksen   842 7月  18 15:27 mycangls

```
- 创建硬链接会增加额外的记录项来引用文件
- 对应同一文件系统上的一个物理文件
- 具有相同的`inode`(节点编号)的多个文件互为硬链接
- 删除源文件对其它硬链接文件没有影响
- 硬链接是源文件的一个入口，可以给文件设置硬链接来防止被误删除
- 删除硬链接文件或者删除源文件，文件实体并不会别删除
- 只有删除源文件和所有的链接文件，文件实体才会被删除
- 不能对目录进行硬链接
- 不能对跨分区进行硬链接操作
- 硬链接文件是普通文件，可以用`rm`删除 

