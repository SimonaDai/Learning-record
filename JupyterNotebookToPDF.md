# Jupyter Notebook  导出 中文PDF


> * 如果想要输出美观PDF，直接看方案二
> * 如果只是能看就行，请看方案一
> * 两种方法均推荐，各有所长！

>  [参考]
>
> https://blog.csdn.net/m0_62443558/article/details/141529840
>
> https://zhuanlan.zhihu.com/p/50297880/
>
> https://blog.csdn.net/weixin_51613747/article/details/133239129

## 方案一：先导出为HTML，再打印PDF

* 优点：这种方法简单快捷，不需要进行很多配置。
* 缺点：可能打印不全（这个问题对于大文件来说，很严重）

第一步：找到标题栏File->Save and Export **Notebook** As->HMTL，导出HTML文件。

![](https://i-blog.csdnimg.cn/direct/e7298ac9e6334a4f9ca2940feb5b5755.png)

第二步：导出为HTML文件后，打开文件。右键进行打印，或者CTRL+P 打印即可。

## 方案二：直接导出PDF

 **初次配置繁琐** ，但是 **美观好看** ，有**书签！**

### 1. 安装**pandoc**

[https://github.com/jgm/pandoc/releases](https://github.com/jgm/pandoc/releases "https://github.com/jgm/pandoc/releases")

要将pandoc路径添加到[环境变量](https://so.csdn.net/so/search?q=%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F&spm=1001.2101.3001.7020)->系统变量->Path下。

### 2. 安装[MiKTex](https://so.csdn.net/so/search?q=MiKTex&spm=1001.2101.3001.7020)

[https://miktex.org/download](https://miktex.org/download "https://miktex.org/download")

安装完成后，也要将Miktex路径添加到环境变量。确保已经添加

我的路径配置如下，大家可以查找自己的文件夹路径。

![](https://i-blog.csdnimg.cn/direct/288386805bf54e6794ac0b5cd2d54eda.png)

### 3.安装宏包

在jupyter notbook中点击File->Download as->PDF

开始出现下载宏包的提示：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/54969f70df09c823f59027b960bc511b.png)
继续安装好多个宏包才完成最终的安装，这样就可以完成全英文文档的转pdf。如果需要转换为中文文档。

### 4.将中文文档转换为PDF

> 注意文件名最好不要是中文！！！

方法是直接修改tex模版文件。

1. 首先找到 ==**index.tex.j2 文件**==。我的 Anaconda 中的虚拟环境路径是 > D:\anaconda3\envs\cn\share\jupyter\nbconvert\templates\latex\index.tex.j2。
2. 找到这部分内容进行替换，其中11pt是字体大小。

```delphi
((*- block docclass -*))
\documentclass[11pt]{ctexart}
((*- endblock docclass -*))


\usepackage{fontspec, xunicode, xltxtra}

\setmainfont{Microsoft YaHei}

\usepackage{ctex}
```

修改后文件内容如下：

![](https://i-blog.csdnimg.cn/direct/67d813f234c94547b1952992e939e89d.png)

在完成修改后，在[jupyter notebook](https://so.csdn.net/so/search?q=jupyter%20notebook&spm=1001.2101.3001.7020)就可以顺利打印。也可能再次弹出宏包下载的提示框，继续下载就行。

### 总结

 配置环境内容很多，效果是很美观的，效果如下：

> 注意： **文件名最好不要是中文** ，可能会报错！！！

![](https://i-blog.csdnimg.cn/direct/cf1649e5f02a430d8170b4d64407b57e.png)



## 问题1 Jupyter Notebook中 Save and Export Notebook As 不显示选项

Jupyter **Notebook**中 Save and Export Notebook As 不显示选项（保存和导出没有选项）
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/9b71a1887b9d433b904b90a01ce204a8.png)

### 解决

在[jupyter notebook](https://so.csdn.net/so/search?q=jupyter%20notebook&spm=1001.2101.3001.7020)所在环境卸载 `jupyter_contrib_nbextensions`，这是我之前安装的一个扩展[工具集](https://so.csdn.net/so/search?q=%E5%B7%A5%E5%85%B7%E9%9B%86&spm=1001.2101.3001.7020)，从而导致上面的问题。

```python
pip uninstall jupyter_contrib_nbextensions
```

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/ac9eca7609f14b97879b1a88c51e5c6b.png)

> **备注：**不显示导出PDF、html 格式，可以删除插件pip uninstall jupyter_contrib_nbextensions
>
> ==安装后必须要配置环境变量path==



# Jupyter Notebook 怎么显示环境内核

> [参考]
>
> https://blog.csdn.net/2303_79392101/article/details/146781559
>
> https://blog.csdn.net/qiufo/article/details/145607267
>
> https://blog.csdn.net/rzjslSe/article/details/146980539

## 1、传统方法（可能存在问题，不推荐）

首先在新建的环境下，安装内核。再将当前 Python 环境注册为 Jupyter Notebook 的一个内核，并命名为 "py3.9"（可以自定义）。

```cobol
#进入py3.9环境，安装内核包，再将当前 Python 环境注册为Jupyter的一个内核，并命名为 "py3.9"



conda activate py3.9



conda install ipykernel



python -m ipykernel install --user --name py3.9 --display-name py3.9
```

 之后可以利用下面的代码查看jupyter内核，可以看到多出来的jupyter内核。

```csharp
#查看内核列表



jupyter kernelspec list
```

![img](https://i-blog.csdnimg.cn/direct/5ebaa39810db40679cb7dd0119f35438.png)

 也可以在jupyter中查看，记得刷新一下页面。

![img](https://i-blog.csdnimg.cn/direct/c5e6d0a442d94608ace27b42cf0df27c.png)

***\*存在问题\****：存在多个不同版本的python同时存在时会出现jupyter连接不上内核和内核长期无响应的问题。

![img](https://i-blog.csdnimg.cn/direct/2025805c04254976baf9b725df57b856.png)

## 2、最佳方法（使用 nb_conda_kernels）——已实践

给环境安装内核，同时将环境添加到jupyter中来。此处作者使用nb_conda_kernels 添加所有环境。这也是防止后期多个python环境同时存在时内核无法连接的最好解决方法。

**首页在新环境中安装内核，再退出新环境来到base环境，安装nb_conda_kernels 添加所有环境！！！**

这是目前作者发现解决多内核（多python环境）情况下，最好解决jupyter连接不上内核的方法。

> 注意：==只运行conda install nb_conda_kernels，启动jupyter notebook不会显示已创建的所有环境，还要在每个环境中分别安装ipykernel==。

```csharp
#在py3.9的新环境中安装内核，并退出环境

conda activate py3.9 
conda install ipykernel
conda deactivate


# 在 base 环境安装 nb_conda_kernels，添加所有环境到jupyter中，并打开jupyter
    
conda activate base     
conda install nb_conda_kernels
jupyter notebook
```

此时进入jupyter浏览器会发现多出了一个 Python[conda env py3.9]，这是py3.9所对应的内核在jupyter中的显示。

![img](https://i-blog.csdnimg.cn/direct/c4047ada309d4fcca716e1ef209d6ca8.png)

可以点击创建新的jupyter文件进行代码的尝试，检验jupyter是否可用。可以在新创建的文件中尝试1+1的简单计算进行检验。

![img](https://i-blog.csdnimg.cn/direct/f59e4ce19cdd469888c908a0f399cfe8.png)

## 内核与环境清理

### 1.删除**Jupyter**内核 

首先查看内核列表，选择你要删除的内核。

```csharp
#首先查看内核列表
jupyter kernelspec list 

#删除名为py3.9的jupyter内核
jupyter kernelspec uninstall py3.9
```

示例： 

![img](https://i-blog.csdnimg.cn/direct/8b7298152f4246ea9046777537ecf005.png)

###  2.删除环境

```cobol
#移除py3.9环境 

conda remove -n py3.9 --all 
```













