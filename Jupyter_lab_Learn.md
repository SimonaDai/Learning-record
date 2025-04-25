# jupyterlab的安装与使用

---

## jupyterlab 介绍和面板分析

JupyterLab有以下特点：

- **交互模式：**[Python交互式模式](https://zhida.zhihu.com/search?content_id=240790142&content_type=Article&match_order=1&q=Python交互式模式&zhida_source=entity)可以直接输入代码，然后执行，并立刻得到结果，因此Python交互模式主要是为了调试Python代码用的
- **内核支持的文档：**使你可以在可以在Jupyter内核中运行的任何文本文件（[Markdown](https://zhida.zhihu.com/search?content_id=240790142&content_type=Article&match_order=1&q=Markdown&zhida_source=entity)，Python，R等）中启用代码
- **模块化界面：**可以在同一个窗口同时打开好几个notebook或文件（HTML, TXT, Markdown等等），都以标签的形式展示，更像是一个IDE
- **镜像notebook输出：**让你可以轻易地创建仪表板
- **同一文档多视图：**使你能够实时同步编辑文档并查看结果
- **支持多种数据格式：**你可以查看并处理多种数据格式，也能进行丰富的可视化输出或者Markdown形式输出
- **云服务：**使用Jupyter Lab连接Google Drive等服务，极大得提升生产力

### 安装Jupyter Lab

你可以使用 `pip`、`conda`安装Jupyter Lab

**pip**
`pip`可能是大多数人使用包管理工具，如果使用 `pip`安装，请在命令行执行：

```text
pip install jupyterlab
```

**conda**
如果你是[Anaconda](https://zhida.zhihu.com/search?content_id=240790142&content_type=Article&match_order=1&q=Anaconda&zhida_source=entity)用户，那么可以直接用 `conda`安装，请在命令行执行：

```text
conda install -c conda-forge jupyterlab
```

### 运行Jupyter Lab

在安装Jupyter Lab后，接下来要做的是运行它。
你可以在命令行使用 `jupyter-lab`或 `jupyter lab`命令，然后默认浏览器会自动打开Jupyter Lab。

![img](https://pic3.zhimg.com/v2-1acef3c62334a0096269490153a49712_1440w.jpg)

![img](https://pic4.zhimg.com/v2-83398e84480a7c07eb2506c2bd214a75_1440w.jpg)

**启动器**
右侧的选项卡称为启动器，你可以新建notebook、console、teminal或者text文本。
当你创建新的notebook或其他项目时，启动器会消失。 如果您想新建文档，只需单击左侧红圈里的“ +”按钮。

![img](https://picx.zhimg.com/v2-5bf604d8a12b4f70b83baa3b178c655d_1440w.jpg)

**打开文档**
在启动器中点击你想要打开的文档类型，即可以打开相应文档。

![img](https://pic2.zhimg.com/v2-2850f3244ddf48ea1002bde7e86beda1_1440w.jpg)

单击左侧的“ +”按钮，新建多个文档，你会看到：

![img](https://pica.zhimg.com/v2-bf45563b092a8b86a63944dfa53ef008_1440w.jpg)

你还可以使用顶部的菜单栏创建新项目，步骤：file->new，然后选择要创建的文档类型。这和Jupyter Notebook一样，如果你经常使用Notebook，那么应该不会陌生。

你可以打开多个文档后，任何排版组合，只需按住选项卡拖移即可。

![img](https://pic2.zhimg.com/v2-91c98244a413cc36c62815e3ed1028e7_1440w.jpg)

当在一个notebook里面写代码时，如果想要实时同步编辑文档并查看执行结果，可以新建该文档的多个视图。步骤：file->new view for notebook

![img](https://pic1.zhimg.com/v2-38d0aa50f61c68c01c433e2332802a3c_1440w.jpg)

**文件浏览器**

左侧一栏是文件浏览器，显示从JupyterLab启动的位置可以使用的文件。

![img](https://pic4.zhimg.com/v2-e04a74e3ba704e41dc0c74a455f59df9_1440w.jpg)

你可以创建文件夹、上传文件并、新文件列表

![img](https://pic2.zhimg.com/v2-637fa95bc332ab8d73f8c03970e8df43_1440w.jpg)

**预览Markdown文本**

![img](https://picx.zhimg.com/v2-ca840fc97dd3a67806b71d71bac099cb_1440w.jpg)

**编辑代码**

![img](https://pic2.zhimg.com/v2-70e9edd7d935232ca3fa1a7916af74c5_1440w.jpg)

**预览csv文件**

![img](https://pic1.zhimg.com/v2-54ddbde336faf7af9c97c6b0098897b4_1440w.jpg)

**预览geojson文件**

![img](https://pic3.zhimg.com/v2-420c86ca5b675995c29a1637569cf9ec_1440w.jpg)

**打开学习文档**
Jupyter Lab支持打开pandas、numpy、matplotlib、scipy、python、ipython、scipy、markdown、notebook等官方文档。步骤：help->选择相应文档

![img](https://pic1.zhimg.com/v2-9ca4b02fd1abe1bb6b0c9bef85d00288_1440w.jpg)

![img](https://pic4.zhimg.com/v2-39197f2ff4e379a8c296ac82bd5083b5_1440w.jpg)

**切换背景主题**
Jupyter Lab支持两种背景主题，白色和黑色。步骤：settings->jupyterlab theme

![img](https://picx.zhimg.com/v2-4f7f0c8f405200968415ef9240a29c39_1440w.jpg)

---

## jupyterlab的安装与使用攻略（Linux）

### 安装JupyterLab

### **更新Jupyter Notebook**

安装 `JupyterLab`需要预先安装4.3或更新版本的 `Jupyter Notebook`，可以用下面的命令查看当前版本：

```bash
jupyter notebook --version
```

### **通过conda安装**

```text
conda install -c conda-forge jupyterlab
```

### **通过pip安装**

```text
pip install jupyterlab
```

### 启动JupyterLab

启动 `JupyterLab`和启动 `Jupyter Notebook`一样简单，只需要在命令行中输入下面的指令，`JupyterLab`就会在默认浏览器中打开。

```text
jupyter lab
```

启动后，`JupyterLab`默认的URL为

```text
http://localhost:8888/lab
```

如果用不惯Lab，还是想用Notebook的话，可以手动把 `/lab`改为 `/tree`，从而切换回经典Notebook的界面。

### 将Conda环境添加到Jupyter Lab中

现在，我们已经创建了一个Conda环境并安装了Jupyter Lab，接下来我们将把这个环境添加到Jupyter Lab中。

首先，我们需要在已激活的环境中安装Jupyter Lab的内核。运行以下命令：

```python
python -m ipykernel install --user --name notebook_env --display-name "机器学习"
```

上述命令将在Jupyter Lab中安装一个新的内核，并将其命名为”机器学习”，其中notebook_env 是我们之前创建的环境名称。

> - user表示为当前用户添加内核，也可以使用--sys-prefix等其他选项根据具体需求选择安装位置。
> - name用于指定内核的名称，在Jupyter Lab中通过该名称识别内核。

然后，我们需要安装nb_conda_kernels扩展。运行以下命令：

```python
conda install nb_conda_kernels
```

运行以上命令后，我们需要重新启动Jupyter Lab。在重新启动之后，我们可以在Jupyter Lab的界面中看到一个下拉菜单，里面包含我们之前创建的Conda环境。

现在，我们可以选择任意一个Conda环境，并在Jupyter Lab中打开一个新的Notebook来使用它。在Notebook中，我们可以导入所需的包和模块，并使用环境中已安装的任何工具和库。

如何查看kernel列表并且删掉确定kernel：

1、查看jupyter kernel的list

```python
jupyter kernelspec list
```

2、移除掉对应的kernel

```python
jupyter kernelspec remove notebook_env
```

## [Linux 配置 jupyter lab参考]

### 1、准备

    本教程是适用于`Linux`操作系统的 `jupyterlab`部署教程，需要提前安装 `Python3`运行环境，可以是基本的 `Python3`、`Anaconda`和 `MiniConda`等 `Python3`环境，需要有良好的网络环境。

### 2、安装 `jupyterlab`

```bash
pip install jupyterlab # 安装jupyter
pip install jupyterlab-language-pack-zh-CN # 安装汉化包，需要自己选择语言
12
```

### 3、生成配置文件

```bash
jupyter lab --generate-config
1
```

上面命令会生成 `jupyterlab`配置文件，路径为 `~/.jupyter/jupyter_lab_config.py`

### 4、创建密码

```bash
jupyter lab password
1
```

填写密码并确认密码，会生成 `~/.jupyter/jupyter_server_config.json`

查看文件内容，如下图，复制 `password`后的一串字符
![img](https://i-blog.csdnimg.cn/blog_migrate/7ce9eb6502641b76599918dba8db1893.png)

### 5、修改配置文件

```bash
vim  ~/.jupyter/jupyter_lab_config.py
1
```

追加以下内容：

```python
c.ServerApp.allow_remote_access = True  # 允许远程访问
c.ServerApp.allow_root = True           # 允许root运行
c.ServerApp.notebook_dir = u'工作文件夹'  # 设置工作目录，默认为用户家目录
c.ServerApp.ip = '*'                    # 监听地址
c.ServerApp.port = 8888                 # 运行端口，默认8888
c.ServerApp.password = '刚复制的字符串'    # 密码
c.ServerApp.open_browser = False        # 不打开浏览器
1234567
```

### 6、后台启动

```bash
nohup python -m jupyterlab --allow-root > ~/.jupyter/jupyter.log 2>&1 &
1
```

    此处利用`nohup`命令让 `jupyterlab`在后台执行，并输出日志到 `~/.jupyter/jupyter.log`文件中，该串代码运行后会输出 `jupyterlab`的进程号，通过进程号，可以使用 `kill -9 进程号`来终止项目，如下图，`4094`即是此次 `jupyterlab`的进程号，使用 `kill -9 4094`即可停止后台运行的 `jupyterlab`。
![img](https://i-blog.csdnimg.cn/blog_migrate/d34ce6841730d701495095f7589283d4.png)

启动后，通过 `IP:端口号`即可进行访问，访问后需要输入之前设置的密码，然后进入的主页面如图所示：

![image-20220831152742285](https://i-blog.csdnimg.cn/blog_migrate/48f8de3888ed02896e7c61bb20d80e76.png)

### 7、终止后台运行的 `jupyterlab`

   使用 `ps -al`命令查看进程号，即 `PID`，然后使用 `kill`命令终止。若想重新启动，再重新运行命令
即可。

```bash
(base) [root@0ca82869d78e ~]# ps -al #查看进程
F S   UID    PID   PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
4 S     0 184175 184005  1  80   0 - 90168 ep_pol pts/2    00:00:03 python
0 R     0 184429 184005  0  80   0 - 12402 -      pts/2    00:00:00 ps
1234
kill -9 184175 # 结束进程
1
```

### 8、切换中文界面

若需中文，使用以下命令安装中文包后，在 `jupyterlab`界面中切换
![img](https://i-blog.csdnimg.cn/blog_migrate/b8bfd0dc3c0ff0e9ec4d9fe176e23930.png)

### 9、安装扩展

    `jupyterlab`相比于传统的 `jupyter notebook`，最大的变化在于支持安装扩展，但很多扩展的安装需要先安装 `node.js`和 `npm`，以下介绍如何安装，若需求较少，可以跳过此步骤。

#### （1）下载并安装 `Nodejs`

##### ① 下载

`node.js`中文官网：[下载 | Node.js 中文网 (nodejs.cn)](http://nodejs.cn/download/)

![image-20220831091237436](https://i-blog.csdnimg.cn/blog_migrate/76ae003ee822c8cffc87d84be5b8f607.png)

访问界面，选择 `Linux 二进制文件 (x64)`，右键 `复制链接`

返回终端，下载：

```bash
wget https://nodejs.org/dist/v16.17.0/node-v16.17.0-linux-x64.tar.xz
1
```

解压：

```bash
tar -xvf ./node-v16.17.0-linux-x64.tar.xz
1
```

移动并重命名

```bash
mv node-v16.17.0-linux-x64/ /opt/nodejs
1
```

##### ② 配置环境变量

```bash
vim /etc/profile
1
```

追加以下内容：

```ini
#set for nodejs
export NODE_HOME=/opt/nodejs
export PATH=$NODE_HOME/bin:$PATH
123
```

使环境变量立即生效

```bash
source /etc/profile
1
```

##### ③ 验证

`nodejs`和 `npm`安装完成，使用以下命令进行验证

```bash
node -v # 查看node.js版本
npm -v  # 查看npm版本
12
```

![image-20220831153329582](https://i-blog.csdnimg.cn/blog_migrate/bb8d10351f175c403427d8718e366a91.png)

##### ④ 换源

若按照速度较慢，可进行换源，此处换成了淘宝源

```bash
npm config set registry http://registry.npmmirror.com
1
```

若想换回官方源：

```bash
npm config set registry https://registry.npmjs.org/
1
```

清除缓存

```bash
npm cache clean --force
1
```

#### （2）安装扩展

如图所示，在 `jupyterlab`界面的右侧即可进行扩展安装

![image-20220831153825545](https://i-blog.csdnimg.cn/blog_migrate/16817a1d7e7167ee1adf8849a4742c4a.png)

### 9、其他问题解决

**问题描述**

```bash
ImportError: IProgress not found. Please update jupyter and ipywidgets. 
See https://ipywidgets.readthedocs.io/en/stable/user_install.html
12
```

#### （1）安装依赖

```bash
pip install ipywidgets widgetsnbextension pandas-profiling
1
```

#### （2）启动 `jupyterlab`相应的插件

```bash
jupyter nbextension enable --py widgetsnbextension
```

---

## 【待学】ssh  时怎么在本机看到远程的jupyter lab 界面

> [参考]https://zhuanlan.zhihu.com/p/356368541

---

## jupyterlab的安装与使用攻略/包括汉化方法（Windows）

> 官网链接[Project Jupyter | Home](https://jupyter.org/index.html)

#### 1.第一步安装

打开控制台

使用pip工具安装

```undefined
pip install jupyterlab
```

 如图![img](https://i-blog.csdnimg.cn/direct/b619554d9194475aaf95d3f6d66c072d.png)

#### 2.安装成功后启动

```undefined
jupyter lab
```

![img](https://i-blog.csdnimg.cn/direct/0b43df8b1ffd48eb8d73f3abe69f8407.png)

会自动启动它的[web页面](https://so.csdn.net/so/search?q=web页面&spm=1001.2101.3001.7020)

然后就可以正常使用咯！！

如果需要更换浏览器访问

新开控制台执行下面命令

```vbscript
jupyter server list
```

 访问：：对该网址进行访问![img](https://i-blog.csdnimg.cn/direct/7a0832040ba7459ea122ce6ded156d04.png)

#### 3.关闭服务

在启动页面使用Ctrl+c 组合键关闭服务。

![img](https://i-blog.csdnimg.cn/direct/d77d96469a2c4457bd74b49f29aa2bf9.png) 重新出现输入提示关闭成功

#### 4.汉化

在控制台内执行

```perl
pip install jupyterlab-language-pack-zh-CN
```

 ![img](https://i-blog.csdnimg.cn/direct/526bae3b48e248a0bd9f88bf6188ac3f.png)

安装成功

启用中文包

```sql
jupyter serverextension enable --py nbTranslate
```

 ![img](https://i-blog.csdnimg.cn/direct/0e64802e27f54ef088a56c799f620954.png)

 然后打开浏览器页面：

1.刷新页面

2.点击setting

3.点击Language，会出现语言[选择框](https://so.csdn.net/so/search?q=选择框&spm=1001.2101.3001.7020)选择中文。

如图：

![img](https://i-blog.csdnimg.cn/direct/87e8e84bf215424693cbb9de25723a2e.png)

切换成功，可以愉快的玩耍了！

效果：

![img](https://i-blog.csdnimg.cn/direct/e28e807586244c739026e649d3ee3498.png)
