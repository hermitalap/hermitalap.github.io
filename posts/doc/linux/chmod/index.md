# 

### 限root权限运行
### 指令
```shell
chmod [-cfvR] [--help] [--version] mode file...
```

例：
```shell
为文件 file1.sh 的拥有者添加该文件的运行权限 :
chmod u+x file1.sh

将文件 file1.txt 设为所有人皆可读取 :
chmod ugo+r file1.txt

将文件 file1.txt 设为所有人皆可读取 :
chmod a+r file1.txt

将文件 file1.txt 与 file2.txt 设为该文件拥有者，与其所属同一个群体者可写入，但其他以外的人则不可写入 :
chmod ug+w,o-w file1.txt file2.txt

为 ex1.py 文件拥有者增加可执行权限:
chmod u+x ex1.py

将目前目录下的所有文件与子目录皆设为任何人可读取 :
chmod -R a+r *

此外chmod也可以用数字来表示权限如 :
chmod 777 file

语法为：
chmod abc file

其中a,b,c各为一个数字，分别表示User、Group、及Other的权限。
```
 r=4，w=2，x=1

-   若要 rwx 属性则 4+2+1=7；
-   若要 rw- 属性则 4+2=6；
-   若要 r-x 属性则 4+1=5。


|#	|权限	|rwx	|二进制|
|---|--|--|--|
|7|	读 + 写 + 执行|	rwx|	111|
|6|	读 + 写|	rw-	|110|
|5|	读 + 执行|	r-x	|101|
|4|	只读|	r--	|100|
|3|	写 + 执行|	-wx	|11|
|2|	只写|	-w-	|010|
|1|	只执行|	--x	|1|
|0|	无|	---	|0|



### 参数
其中：

-   u 表示该文件的拥有者，g 表示与该文件的拥有者属于同一个群体(group)者，o 表示其他以外的人，a 表示这三者皆是。
-   \+ 表示增加权限、- 表示取消权限、= 表示唯一设定权限。
-   r 表示可读取，w 表示可写入，x 表示可执行，X 表示只有当该文件是个子目录或者该文件已经被设定过为可执行。

其他参数说明：

-   -c : 若该文件权限确实已经更改，才显示其更改动作
-   -f : 若该文件权限无法被更改也不要显示错误讯息
-   -v : 显示权限变更的详细资料
-   -R : 对目前目录下的所有文件与子目录进行相同的权限变更(即以递归的方式逐个变更)
-   --help : 显示辅助说明
-   --version : 显示版本
