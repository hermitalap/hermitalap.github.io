# 

## 简介
项目地址：https://github.com/schollz/croc
使用方法：发送端选择需要发送的文件，设置一串口令，或者使用程序自动生成的随机口令，接收端输入该口令后，两台设备立即连接，建立点对点传输，完成文件传输。

### 安装方法：
Download [the latest release for your system](https://github.com/schollz/croc/releases/latest), or install a release from the command-line:

```
curl https://getcroc.schollz.com | bash
```

On macOS you can install the latest release with [Homebrew](https://brew.sh/):

```
brew install croc
```

On macOS you can also install the latest release with [MacPorts](https://macports.org/):

```
sudo port selfupdate
sudo port install croc
```

On Windows you can install the latest release with [Scoop](https://scoop.sh/) or [Chocolatey](https://chocolatey.org/):

```
scoop install croc
```

```
choco install croc
```

### 使用方法：
最简单的传输一个文件或者文件夹:

```
$ croc send [file(s)-or-folder]
Sending 'file-or-folder' (X MB)
Code is: code-phrase
```

然后在接受设备接受这个文件或者文件夹，只需要：

```
croc code-phrase
```

**code-phrase**是自动生成的密文

代码短语用于建立密码验证密钥协议 ( [PAKE](https://en.wikipedia.org/wiki/Password-authenticated_key_agreement) )，该协议为发送方和接收方生成用于端到端加密的密钥。

有许多可配置的选项（请参阅 参考资料`--help`）。一组选项（如自定义中继、端口和代码短语）可以使用`--remember`.

### 自定义代码短语

您可以使用自己的密码短语发送（必须超过 6 个字符）。

```
croc send --code [code-phrase] [file(s)-or-folder]
```

## 补充的使用方法

### [](https://github.com/schollz/croc#allow-overwriting-without-prompt)允许在没有提示的情况下覆盖

默认情况下，croc 会提示是否覆盖文件。您可以使用该`--overwrite`标志（仅限收件人）自动覆盖文件。例如，接收文件以自动覆盖：

```
croc --yes --overwrite <code>
```

### [](https://github.com/schollz/croc#use-pipes---stdin-and-stdout)使用管道 - stdin 和 stdout

您可以通过管道连接到`croc`：

```
cat [filename] | croc send
```

在这种情况下，`croc`将自动使用标准输入数据并发送和分配一个文件名，如“croc-stdin-123456789”。要接收到`stdout`，您可以随时使用`--yes` will 自动批准转移并将其通过管道发送到`stdout`。

```
croc --yes [code-phrase] > out
```

打印到控制台的所有其他文本`stderr`都将转到`stdout`.

### [](https://github.com/schollz/croc#send-text)发短讯

有时您想发送 URL 或短文本。除了管道之外，您还可以使用以下命令轻松发送文本`croc`：

```
croc send --text "hello world"
```

这将自动告诉接收者`stdout`在收到文本时使用，以便显示。

### [](https://github.com/schollz/croc#use-a-proxy)使用代理

您可以通过添加代理地址来使用代理作为与中继的连接`--socks5`。例如，您可以通过 tor 中继发送：

```
croc --socks5 "127.0.0.1:9050" send SOMEFILE
```

### [](https://github.com/schollz/croc#change-encryption-curve)更改加密曲线

您可以使用`--curve`标志从几个不同的椭圆曲线中进行选择以用于加密。只有收件人可以选择曲线。例如，使用 P-521 曲线接收文件：

```
croc --curve p521 <codephrase>
```

可用曲线有 P-256、P-348、P-521 和 SIEC。SIEC 是使用的默认曲线，它是一种鲜为人知的曲线，属于一类“超隔离”曲线，其安全性不会降低到其周围曲线的安全性。(Scholl, Travis. 实验数学 28.4 (2019): 385-397)

### [](https://github.com/schollz/croc#self-host-relay)自主机中继

需要继电器来装订并行的传入和传出连接。默认情况下，`croc`使用公共中继，但您也可以运行自己的中继：

```
croc relay
```

默认情况下，它使用 TCP 端口 9009-9013。确保打开它们。您可以自定义端口（例如`croc relay --ports 1111,1112`），但必须至少有**2 个**用于中继的端口。第一个端口用于通信，后续端口用于多路复用数据传输。

`--relay`如果您想自定义主机，您可以通过输入更改您正在使用的中继来使用您的中继发送文件。

```
croc --relay "myrelay.example.com:9009" send [filename]
```

注意，发送时只需要包含第一个端口（通信端口）即可。用于数据传输的后续端口将从中继传输回用户。

#### [](https://github.com/schollz/croc#self-host-relay-docker)自主机中继（docker）

如果更简单，您还可以使用 Docker 运行中继：

```
docker run -d -p 9009-9013:9009-9013 -e CROC_PASS='YOURPASSWORD' schollz/croc
```

请务必包含中继的密码，否则任何请求都将被拒绝。

```
croc --pass YOURPASSWORD --relay "myreal.example.com:9009" send [filename]
```

注意：当包含时，`--pass YOURPASSWORD`您可以改为传递带有密码的文件，例如`--pass FILEWITHPASSWORD`.
