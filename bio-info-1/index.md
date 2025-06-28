# Day 1 Linux基本命令

### ⚠️ 小提示：脚本中的相对路径

如果你在脚本中用的是相对路径（比如 `./data/input.txt`），那么脚本运行时的“当前工作目录”就会影响它的行为。

为避免出错，可以在脚本开头加一句让路径自动转为脚本自身所在目录：

```bash
bash
复制编辑
DIR="$(cd "$(dirname "$0")" && pwd)"

```

然后用 `${DIR}/data/input.txt` 来引用脚本目录下的文件。

### 在 **终端命令行（如 bash/zsh）**：

- **`Ctrl + U`**：删除光标前的所有字符
- **`Ctrl + K`**：删除光标后的所有字符
- **`Ctrl + A`**：移动到行首（可搭配 Ctrl+K）
- **`Ctrl + E`**：移动到行尾

### 示例：一键删除整行

```bash

Ctrl + A → Ctrl + K
```

### 🧭 文件/目录查看与导航

| 命令 | 全称 | 作用 | 常见用法 |
| --- | --- | --- | --- |
| `ls` | **list** | 列出目录内容 | `ls -l` 查看详细信息`ls -a` 显示隐藏文件 |
| `cd` | **change directory** | 切换当前工作目录 | `cd /path/to/dircd ..` 返回上一级 |
| pwd | print work directory | 打印当前工作目录 |  |

---

### 🔁 文件与目录操作

| 命令 | 全称 | 作用 | 常见用法 |
| --- | --- | --- | --- |
| `mv` | **move** | 移动或重命名文件/目录 | `mv a.txt b.txt` 重命名`mv a.txt dir/` 移动 |
| `cp` | **copy** | 复制文件或目录 | `cp a.txt b.txtcp -r dir1 dir2` 递归复制目录 |
| `rm` | **remove** | 删除文件或目录 | `rm a.txt` 删除文件`rm -rf dir/` 强制删除目录 |
| `mkdir` | **make directory** | 创建目录 | `mkdir newdirmkdir -p a/b/c` 创建多级目录 |
| `rename` | **rename**（并非 GNU 标准一部分） | 批量重命名文件（需安装） | `rename 's/.txt/.bak/' *.txt` |

---

### 📄 文件查看与编辑

| 命令 | 全称 | 作用 | 常见用法 |
| --- | --- | --- | --- |
| `cat` | **concatenate** | 查看、连接文件内容 | `cat file.txt` 查看文件`cat a b > c` 合并 |
| `nano` | **Nano text editor** | 命令行文本编辑器 | `nano file.txt` 编辑文件 |
| `touch` | **touch file timestamp** | 创建空文件或更新修改时间 | `touch new.txt` 创建新文件或刷新时间戳 |

---

### 📝 示例场景

```bash
bash
复制编辑
mkdir projects              # 创建目录
cd projects                 # 进入目录
touch README.md             # 创建文件
nano README.md              # 编辑文件
ls -l                       # 查看当前目录内容
cp README.md copy.md        # 复制文件
mv copy.md docs.md          # 重命名文件
rm docs.md                  # 删除文件

```

- 
- `ls`
    
    查看当前目录下的文件和目录
    
    ```bash
    
    ls            # 简单列出
    ls -l         # 详细信息（权限、大小、修改时间）
    ls -a         # 显示隐藏文件
    
    ```
    
- `cd`
    
    切换目录
    
    ```bash
    
    cd /path/to/directory
    cd ..         # 返回上一级目录#cd后有一个空格
    cd ~          # 回到当前用户主目录
    
    ```
    

---

### 🔁 文件/目录操作

- `cp`
    
    复制文件或目录
    
    ```bash
    
    cp file1.txt file2.txt                 # 复制文件
    cp file1.txt /path/to/destination/     # 复制到指定目录
    cp -r dir1/ dir2/                      # 递归复制目录
    
    ```
    
- `mv`
    
    移动或重命名文件/目录
    
    ```bash
    
    mv file.txt /path/to/destination/      # 移动
    mv oldname.txt newname.txt             # 重命名
    
    ```
    
- `rm`
    
    删除文件或目录
    
    ```bash
    
    rm file.txt             # 删除文件
    rm -r folder/           # 递归删除目录
    rm -rf folder/          # 强制删除，不提示
    
    ```
    
- `rename`
    
    批量重命名文件（需安装 `rename` 工具）
    
    ```bash
    
    rename 's/.txt/.bak/' *.txt  # 将所有 .txt 文件扩展名改为 .bak
    
    ```
    

---

### 🛠️ 文件内容处理与编辑

- `cat`
    
    查看文件内容（或合并文件）
    
    ```bash
    
    cat file.txt
    cat file1.txt file2.txt > merged.txt
    
    ```
    
- `nano`
    
    终端内简单文本编辑器
    
    ```bash
    
    nano file.txt
    
    ```
    
- `touch`
    
    创建空文件，或更新已有文件的时间戳
    
    ```bash
    
    touch newfile.txt
    
    ```
    

### 📁 `mkdir` – 创建目录（文件夹）

`mkdir`（**make directory**）用于在 Linux 中创建一个或多个新目录。

### ✅ 基本用法：

```bash

mkdir my_folder         # 创建一个名为 my_folder 的新目录

```

## *通配符的作用

- 匹配 **0个或多个任意字符**
- 常用于匹配文件名、路径名、样本名等

---

### ✅ 举例说明：

### 📁 假设当前目录下有这些文件：

```

sample1_R1.fastq.gz
sample1_R2.fastq.gz
sample2_R1.fastq.gz
sample2_R2.fastq.gz
notes.txt

```

### 示例 1：匹配所有 `.fastq.gz` 文件

```bash

ls *.fastq.gz

```

➡️ 输出：

```

sample1_R1.fastq.gz
sample1_R2.fastq.gz
sample2_R1.fastq.gz
sample2_R2.fastq.gz

```
