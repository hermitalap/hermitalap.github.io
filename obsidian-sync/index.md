# Obsidian-免费的多设备同步


### 将vault备份到GitHub

![](Pasted%20image%2020210907165301.png "一个新的库，包含一些文档和图片")

首先关闭安全模式

![](Pasted%20image%2020210907165412.png "安装第三方插件，关闭安全模式")


![](Pasted%20image%2020210907165453.png "关闭安全模式")

然后在第三方插件库中下载这个插件

![](Pasted%20image%2020210907165611.png "搜索关键词git，安装Obsidian Git")

启用插件

![](Pasted%20image%2020210907165715.png " 记得启用")

然后需要注意的是该插件不能自己创建git repository，需要你自己先创建一个。

因为我们需要上传备份到GitHub，所以直接下载[GitHub Desktop](https://desktop.github.com/)

如果还没有账号，需要注册一个自己的GitHub账号

进入GitHub Desktop后，先登录自己的账号，然后左上角File-New repository

![](Pasted%20image%2020210907170850.png "")

Path定位到你的库文件夹**所在的父文件夹**，然后Name需要和你的vault文件夹名称**完全相同**，其他的随便填。

![](Pasted%20image%2020210907172037.png "")

现在需要把你的这个repository发布到GitHub的服务器上，点击`Publish repository`

![](Pasted%20image%2020210907171540.png "")


![](Pasted%20image%2020210907172445.png "勾选Keep this code private")

此时登录GitHub，已经可以看到你的repository了。

![](Pasted%20image%2020210907173231.png "")

现在回到Obsidian，进入设置，左边拉到最下面进入Obsidian Git设置项，设置你的自动保存间隔分钟（第一项，Commit git，相当于保存一个可回溯的存档，push：指将这次commit上传到GitHub的服务器上）和自动pull间隔（第二项，即几分钟从服务器上同步到本地一次）

![](Pasted%20image%2020210907173450.png)

然后现在就可以自动备份了，但有时你可能会注意到报错

![](Pasted%20image%2020210907172948.png "报错，无法自动push到GitHub")

这是因为众所周知的原因，git间歇性无法在大陆正常使用，但是如果你有梯子，就可以解决，但是这个插件底端不走梯子的代理，那么手动用GitHub Desktop的push是走梯子的代理的。进入GitHub Desktop，然后点一下push即可

![](Pasted%20image%2020210907174802.png "手动push上传")
