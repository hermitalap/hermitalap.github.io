# RNA-seq基础-1-环境配置

Miniconda是Anaconda的基础版，提供环境管理
<!--more-->
### 下载
[Miniconda官网](https://docs.conda.io/en/latest/miniconda.html)
使用最新包的地址下载
```bash
$ wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```
下载完成：
```bash
$ ls
Miniconda3-latest-Linux-x86_64.sh
```

### 安装
```bash
$ sh Miniconda3-latest-Linux-x86_64.sh
  
Welcome to Miniconda3 py39_4.10.3  
  
In order to continue the installation process, please review the license  
agreement.  
Please, press ENTER to continue  
>>>
```
回车继续，然后按空格直接跳到文档底部，输入yes并回车
```bash
Do you accept the license terms? [yes|no]  
[no] >>>yes
```

```bash
Miniconda3 will now be installed into this location:  
/home/xxx/miniconda3  
  
- Press ENTER to confirm the location  
- Press CTRL-C to abort the installation  
- Or specify a different location below  
  
[/home/xxx/miniconda3] >>>
```
之后一路yes回车即可

### 添加国内源
conda默认从国外服务器上下载包，速度较慢，可换为国内源
[清华源](https://mirror.tuna.tsinghua.edu.cn/help/anaconda/)

### 创建新环境
```bash
conda create -n rnaseq python==3.7 -y
```
测试python3.7对各种包的支持较好
完成后，进入该环境
```bash
$ conda activate rnaseq
(rnaseq) xxx@luo-lab-tower:~$
```
命令提示符前的括号表示当前的环境，只有进入到该环境中才可以使用该环境中的包，可以创建多个环境，多个环境之间互不影响。

### 安装hisat2-stringtie分析流程所需的软件包
```bash
(rnaseq) xxx@luo-lab-tower:~$ conda install fastqc -y
```
fastqc 用于检验reads读数质量
用相同办法继续安装：
```bash
hisat2
samtools
stringtie
htseq-count
tqdm
```
参照该博文[安装sratoolkit最新版](https://blog.csdn.net/guguaihezi/article/details/81240916)
官方安装包地址：https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/
最新的应该是2.11.0

{{< admonition tip >}}
完成以上后，自行google了解这些包的主要用途和基本使用方法。
{{< /admonition >}}

