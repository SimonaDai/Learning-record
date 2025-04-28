# TensorBoard 的安装和使用

## TensorBoard 的安装

`TensorBoard`是一个可视化的模块，该模块功能强大，可用于深度学习网络模型训练查看模型结构和训练效果（预测结果、网络模型结构图、准确率、`loss`曲线、学习率、权重分布等），可以帮你更好的了解网络模型，设计 `TensorBoard`调用相关代码，以上结果即可保存，是整合资料、梳理模型的好帮手。
安装 `TensorBoard`,必须要配一个带GPU的虚拟环境，`tensorflow-gpu`和 `pytorch`的环境选一个就好，配好环境后，下面介绍安装技巧和步骤。

### 安装步骤

1. 可以在激活的命令行中安装：

> conda activate pytorch1.8.0

之后，在命令行中输入：

> pip install tensorboard
> pip install tensorboardX

`Tensorboard`其实是[TensorFlow♂](https://tensorflow.google.cn/guide?hl=zh_cn) 的一个附加工具，**而 `TensorboardX` 这个工具使得 `TensorFlow` 外的其他神经网络框架也可以使用到 `Tensorboard` 的便捷功能，如 `pytorch`**；安装的版本不用管，会自动安装最近的版本，本设备 `pytorch`环境安装情况如下：
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/edf0cce24d44ad92c714edb71a8624a0.png#pic_center)

当然，用一些镜像源可以加速下载，下面给出一些好用的镜像源（清华和豆瓣镜像源比较快）：

> https://pypi.tuna.tsinghua.edu.cn/simple
> https://pypi.douban.com/simple

使用方法在pip安装命令行末尾加（ -i 镜像网址）,`pip`安装其他模块也适用。

> pip install tensorboard -i https://pypi.tuna.tsinghua.edu.cn/simple

1. 编译器自动提醒安装，点击确定安装会在编译器终端自动安装。
2. 编译器终端命令行安装，该方式在编译器中选择带 `GPU`的环境后，不虚激活环境，直接 `pip` 输入命令行直接安装，方法同上述。

**注意：其实其他模块安装包，这些方法基本都适用**

**安装后，在命令行输入：**

```shell
tensorboard --help
```

若可以正常输出，则说明安装成功。

## TensorBoard 的界面介绍

![在这里插入图片描述](https://raw.githubusercontent.com/iioSnail/blogger_res/main/img/9a396452122330006bc424532af6056a.png)

进入tensorboard页面后，啥都看不到，因为我们还没有向log里面写入任何数据：

![在这里插入图片描述](https://raw.githubusercontent.com/iioSnail/blogger_res/main/img/27bf93ccfb0fec42ae0296e2f53ee3f5.png)

使用后续 `add_scalar`准确率折线图：

```python
for i in range(100):
    writer.add_scalar(tag="accuracy", # 可以暂时理解为图像的名字
                      scalar_value=i * random.uniform(0.8, 1),  # 纵坐标的值
                      global_step=i  # 当前是第几次迭代，可以理解为横坐标的值
                      )
    time.sleep(2 * random.uniform(0.5, 1.5))
```

这里模拟1~3秒完成一次迭代并计算准确率，然后将准确率补充到下面这张图。

经过一会后，我们刷新页面，就可以看到我们的准确率变化曲线了：

![在这里插入图片描述](https://raw.githubusercontent.com/iioSnail/blogger_res/main/img/dc82137850733e594239d24745be3796.png)

由于数据仍在写入，所以轮廓仍在不断变化。

> 如何和将多个形状稀疏在一张上？ 答：使用 `writer.add_scalars`即可
>
> 如何将多个图像放在一个标签下？答：在指定标签时，使用同一个父标签，然后使用 `/`分割即可。例如：`tag=record/avg_loss`,`tag=record/total_loss`

**张量折线图**
![在这里插入图片描述](https://raw.githubusercontent.com/iioSnail/blogger_res/main/img/c7022f1f4a4ec56a81933dc45220daa9.png)

## TensorBoard 的使用教程

### TensorBoard 启动

方式**1**

采用Terminal的方案：

![img](https://i-blog.csdnimg.cn/blog_migrate/552f00fa9447f5241b0a89cfec347636.png)

方式**2**

在安装成功之后通过可以通过如下命令来进行测试：

```text
tensorboard --logdir=runs
```

并会出现如下提示：

```powershell
TensorBoard 1.15.0 at http://localhost:6006/ 

(Press CTRL+C to quit)
```

也就是说此时我们便可以通过 `127.0.0.1:6006`这个链接来访问Tensorboard的可视化页面，如图1所示：

![img](https://pic1.zhimg.com/v2-222f7e8a0ddb4e73d5816f375aa68b0e_1440w.jpg)

图 1. Tensorboard启动成功图

如果你发现打不开这里地址，那么可以尝试通过如下命令来进行启动，然后再通过 `127.0.0.1:6006`这个链接来访问。

```ps1con
tensorboard --logdir=runs --host 0.0.0.0
```

> 命令中的 `--logdir`用来指定可视化文件的目录地址

### Tensorboard的使用逻辑

Tensorboard的工作流程简单来说是将代码运行过程中的，某些你关心的数据保存在一个**文件夹**中：这一步由代码中的writer完成，再读取这个**文件夹**中的数据，用浏览器显示出来；这一步通过在命令行运行tensorboard完成。

---

**代码体中要做的事**

首先导入tensorboard

```text
from torch.utils.tensorboard import SummaryWriter
```

这里的SummaryWriter的作用就是，将数据以特定的格式存储到刚刚提到的那个**文件夹**中。

首先我们将其实例化

```text
writer = SummaryWriter('./path/to/log')
```

这里传入的参数就是指向文件夹的路径，之后我们使用这个writer对象“拿出来”的任何数据都保存在这个路径之下。

这个对象包含多个方法，比如针对数值，我们可以调用

```text
writer.add_scalar(tag, scalar_value, global_step=None, walltime=None)
```

这里的tag指定可视化时这个变量的名字，scalar_value是你要存的值，global_step可以理解为x轴坐标。

举一个简单的例子：

```text
for epoch in range(100)
    mAP = eval(model)
    writer.add_scalar('mAP', mAP, epoch)
```

这样就会生成一个x轴跨度为100的折线图，y轴坐标代表着每一个epoch的mAP。这个折线图会保存在指定的路径下（但是现在还看不到）

同理，除了数值，我们可能还会想看到模型训练过程中的图像。

```text
writer.add_image(tag, img_tensor, global_step=None, walltime=None, dataformats='CHW')
 writer.add_images(tag, img_tensor, global_step=None, walltime=None, dataformats='NCHW')
```

---

**可视化**

我们已经将关心的数据拿出来了，接下来我们只需要在命令行运行：

```text
tensorboard --logdir=./path/to/the/folder --port 8123
```

然后打开浏览器，访问地址[http://localhost:8123/](https://link.zhihu.com/?target=http%3A//localhost%3A8123/)即可。这里的8123只是随便一个例子，用其他的未被占用端口也没有任何问题，注意命令行的端口与浏览器访问的地址同步。

如果发现不显示数据，注意检查一下路径是否正确，命令行这里注意是

```text
--logdir=./path/to/the/folder
```

而不是

```text
--logdir= './path/to/the/folder '
```

另一点要注意的是tensorboard并不是实时显示（[visdom](https://zhida.zhihu.com/search?content_id=120089983&content_type=Article&match_order=1&q=visdom&zhida_source=entity)是完全实时的），而是默认30秒刷新一次

### TensorBoard 日志文件加上时间戳

`Step1`:创建日志写入地址，文件夹名为`logs

```
Step1`:创建日志写入地址，文件夹名为`logs
current_time = datetime.datetime.now().strftime("%Y%m%d-%H%M%S")
log_dir = 'logs/' + current_time
summary_writer = tf.summary.create_file_writer(log_dir) 
123
```

`Step2`:喂入监听数据，设置时间戳

```python
        with summary_writer.as_default():
            tf.summary.scalar('train-loss', float(loss_ce), step=epoch) #此处时间戳为epoch
            tf.summary.scalar('test-acc', float(acc), step=epoch)
```

## TensorBoard 中常用函数汇总

进入后打开structure可以查看该包内的对象和方法,比较常用的这几个方法

![img](https://i-blog.csdnimg.cn/blog_migrate/975f984bb89710651671ff91b38f8745.png)

### **3.1 `add_scalar`方法**

这个方法通常用来可视化网络训练时的各类标量参数，例如损失、学习率和准确率等。如下便是 `add_scalar`方法的使用示例：

```python3
1 from torch.utils.tensorboard import SummaryWriter
2 if __name__ == '__main__':   
3     writer = SummaryWriter(log_dir="runs/result_1", flush_secs=120)
4     for n_iter in range(100):
5         writer.add_scalar(tag='Loss/train',
6                           scalar_value=np.random.random(),
7                           global_step=n_iter)
8         writer.add_scalar('Loss/test', np.random.random(), n_iter)
9     writer.close()
```

在上述代码中，第1行用来导入相关的可视化模块；第3行是实例化一个可视化类对象，`log_dir`用于指定可视化数据的保存路径，`flush_secs`表示指定多少秒将数据写入到本地一次（默认为120秒）；第5-7行则是利用 `add_scalar`方法来对相关标量进行可视化，其中 `tag`表示对应的标签信息。

在上述代码运行之前，先进入到该代码文件所在的目录，然后运行如下命令来启动Tensoboard：

```python3
tensorboard --logdir=runs

TensorBoard 1.15.0 at http://localhost:6006/ (Press CTRL+C to quit)
```

可以看出，`logdir`后面的参数就是上面代码第3行里的参数。同时，根据提示在浏览器中打开上述链接便可以看到如图1所示的界面。

接着开始运行上述程序，此时便会在当前目录中生成如图7所示的文件（夹），其中 `result_1`便是前面所指定的子目录，而以 `events.out`开始的文件则是生成的可视化数据文件。

![img](https://picx.zhimg.com/v2-32569afce518d3a68b31fea9fa377a35_1440w.jpg)

图 7. 可视化数据文件图

当程序运行时Tensoboard便会加载图7中所示的文件并在网页端进行渲染，如图8所示：

![img](https://pic3.zhimg.com/v2-0fb9066c2916c32c5d0809d273f132b0_1440w.jpg)

图 8. Tensoboard可视化结果图

如图8所示为Tensoboard的可视化结果图，其中右边的Loss标签就是上面第5行代码中指定的 `Loss/train`参数的前缀部分，也就是说如果想把若干个图放到一个标签下，那么就要保持其前缀一致，例如这里的 `Loss/train`和 `Loss/test`这两个图都将被放在 `Loss`这个标签下。同时，在勾选左上角的"Show data download links"后，还能点击图片下方的按钮来分别下载SVG矢量图、原始图片的CSV或JSON数据。

在图8的左边部分，Smoothing参数用来调整右侧可视化结果的平滑度；Horizontal Axis用来切换不同的显示模式；Runs下面用来勾选需要可视化的结果，例如后续在初始化 `SummaryWriter()`时指定 `log_dir="runs/result_2"`，那么在 `result_1`下方便会再出现一个 `result_2`的选项，这时我们可以选择多个结果同时可视化展示。

下面，掌柜开始逐一介绍几个常用的可视化方法。

### 3.2 `add_graph`方法

从名字可以看出 `add_graph`方法是用于可视化模型的网络结构图，其用法示例如下：

```python3
1 import torchvision
2 def add_graph(writer):
3     img = torch.rand([1, 3, 64, 64], dtype=torch.float32)
4     model = torchvision.models.AlexNet(num_classes=10)
5     writer.add_graph(model, input_to_model=img)  # 类似于TensorFlow 1.x 中的fed
```

为了示例简洁，掌柜这里又把 `SummaryWriter()`中的 `add_graph`方法写成了一个函数。在上述代码中，第4行用于返回一个网络模型；第5行则是对网络结构图进行可视化，其中 `input_to_model`参数为模型所接收的输入，这类似于TensorFlow中的 `fed_dict`参数。

上述代码开始运行之后，便可以在网页端看到如下所示的可视化结果：

![img](https://pic3.zhimg.com/v2-cd0e707c2f8d7ebb1388e65850319ac0_1440w.jpg)

图 9. add_graph可视化结果图

如图9所示便是可视化后的网络结构图，对于右侧网络结构中的每个模块都可以双击进行展开，而左边则是相关模式的切换。

### **3.3 `add_scalars`方法**

这个方法与 `add_scalar`的差别在于 `add_scalars`在一张图中可以绘制多个曲线，我们只需要以字典的形式传入参数即可，如下为 `add_scalars`方法的使用示例：

```python3
 1 def add_scalars(writer):
 2     r = 5
 3     for i in range(100):
 4         writer.add_scalars(main_tag='scalars1/P1',
 5                            tag_scalar_dict={'xsinx': i * np.sin(i / r),
 6                                             'xcosx': i * np.cos(i / r),
 7                                             'tanx': np.tan(i / r)},
 8                            global_step=i)
 9         writer.add_scalars('scalars1/P2',
10                            {'xsinx': i * np.sin(i / (2 * r)),
11                             'xcosx': i * np.cos(i / (2 * r)),
12                             'tanx': np.tan(i / (2 * r))}, i)
13         writer.add_scalars(main_tag='scalars2/Q1',
14                            tag_scalar_dict={'xsinx': i * np.sin((2 * i) / r),
15                                             'xcosx': i * np.cos((2 * i) / r),
16                                             'tanx': np.tan((2 * i) / r)},
17                            global_step=i)
18         writer.add_scalars('scalars2/Q2',
19                            {'xsinx': i * np.sin(i / (0.5 * r)),
20                             'xcosx': i * np.cos(i / (0.5 * r)),
21                             'tanx': np.tan(i / (0.5 * r))}, i)
```

在上述代码中，掌柜一共画了4个图，分别对应代码中的4个 `add_scalars`；同时在每张图里面都都对应了3条曲线，也即 `add_scalars`方法里的 `tag_scalar_dict`参数；并且掌柜这里一共用了2个标签来进行分隔，即 `scalars1`和 `scalars2`。可视化的结果如图10所示。

![img](https://pic2.zhimg.com/v2-f663234ce72ff706712c8a810ceacaa1_1440w.jpg)

图 10. add_scalars可视化结果图

### **3.4 `add_histogram`方法**

直方图的示例用法比较简单， 如下所示：

```python3
1 def add_histogram(writer):
2     for i in range(10):
3         x = np.random.random(1000)
4         writer.add_histogram('distribution centers/p1', x + i, i)
5         writer.add_histogram('distribution centers/p2', x + i * 2, i)
```

可视化后的结果如图11所示。

![img](https://pic1.zhimg.com/v2-597e1c6a07140432e91f9203763840f6_1440w.jpg)

图 11. add_histogram可视化结果图

### **3.5 `add_image`方法**

`add_image`方法是用来可视化相应的像素矩阵，例如本地图片，或者是特征图等

```python3
1 def add_image(writer):
2     from PIL import Image
3     img1 = np.random.randn(1, 100, 100)
4     writer.add_image('img/imag1', img1)
5     img2 = np.random.randn(100, 100, 3)
6     writer.add_image('img/imag2', img2, dataformats='HWC')
7     img = Image.open('./dufu.png')
8     img_array = np.array(img)
9     writer.add_image('local/dufu', img_array, dataformats='HWC')
```

在上述代码中，第3-4行用于生成一个形状为 `[C,H,W]`的3维矩阵并进行可视化；第5-6行则是生成形状为 `[H,W,C]`的3维矩阵并可视化，同时需要在 `add_image`中指定矩阵的维度信息，因此可以看出 `add_image`方法接受的默认格式为 `[C,H,W]`；第7-9行则是先从本地读取一张图片，然后再对其进行可视化，如图12所示。

![img](https://pic4.zhimg.com/v2-318801188c878fb3ed9a2e02267f9e55_1440w.jpg)

图 12. add_image可视化结果图

### **3.6 `add_images`方法**

从名字可以看出，该方法是一次性可视化多张像素图，使用示例如下：

```python3
1 def add_images(writer):
2     img1 = np.random.randn(8, 100, 100, 1)
3     writer.add_images('imgs/imags1', img1, dataformats='NHWC')
4     img2 = np.zeros((16, 3, 100, 100))
5     for i in range(16):
6         img2[i, 0] = np.arange(0, 10000).reshape(100, 100) / 10000 / 16 * i
7         img2[i, 1] = (1 - np.arange(0, 10000).reshape(100, 100) / 10000) / 16 * i
8     writer.add_images('imgs/imags2', img2)  # Default is :math:`(N, 3, H, W)`
```

在上述代码中，第2-3行用于生成8张通道数为1的像素图并进行可视化；第4-8行则是生成16张通道数为3的像素图并进行可视化。最后可视化的结果如图13所示。

![img](https://picx.zhimg.com/v2-2df91cfcd15b24672bf87fe3cab6936b_1440w.jpg)

图 13. add_images可视化结果图

### **3.7 `add_figure`方法**

这个方法的作用是用来将 `matplotlib`包中的 `figure`对象可视化到Tensoboard的网页端，用于展示一些较为复杂的图片，其示例用法如下：

```python3
1 def add_figure(writer):
2     fig = plt.figure(figsize=(5, 4))
3     ax = fig.add_axes([0.12, 0.1, 0.85, 0.8])
4     xx = np.arange(-5, 5, 0.01)
5     ax.plot(xx, np.sin(xx), label="sin(x)")
6     ax.legend()
7     fig.suptitle('Sin(x) figure\n\n', fontweight="bold")
8     writer.add_figure("figure", fig, 4)
9     # plt.show()
```

在上述代码中，第2-7行为根据 `matplotlib`包绘制相应的图像，其中第3行用来指定；第8行则是将其在Tensoboard中进行可视化；第9行则是直接在程序里进行可视化。最后可视化的结果如图14所示。

![img](https://pica.zhimg.com/v2-3fcd5a9261f848f062ae8d22e15bdfc4_1440w.jpg)

图 14. add_figure可视化结果图

如果需要一次在Tensoboard中可视化一组图像的话，可以通过如下方式来进行实现：

```python3
 1 def add_figures(writer, images, labels):
 2     text_labels = ['t-shirt', 'trouser', 'pullover', 'dress', 'coat',
 3                    'sandal', 'shirt', 'sneaker', 'bag', 'ankle boot']
 4     labels = [text_labels[int(i)] for i in labels]
 5     fit, ax = plt.subplots(len(images) // 5, 5, figsize=(10, 2 * len(images) // 5))
 6     for i, axi in enumerate(ax.flat):
 7         image, label = images[i].reshape([28, 28]).numpy(), labels[i]
 8         axi.imshow(image)
 9         axi.set_title(label)
10         axi.set(xticks=[], yticks=[])
11     writer.add_figure("figure", fit)
```

在上述代码中，掌柜选择是的FashionMNIST数据集进行的可视化；第5行代码用来生成一个包含有过个子图的画布；第6-10行是分别用来画出每一个子图；第10行用来去掉横纵坐标的信息；第11行则是将其在Tensoboard中进行展示。最终可视化后的结果如图15所示。

![img](https://pic4.zhimg.com/v2-307dcf0a8868c9f8f7950e69f6b510c3_1440w.jpg)

图 15. add_figure可视化结果图

### **3.8 `add_pr_curve`方法**

`add_pr_curve`这个方法是用来在训练过程中可视化Precision-Recall曲线，即观察在不同阈值下精确率与召回率的平衡情况。更多关于Precision-Recall曲线内容的介绍可以参考文章[详解机器学习中的Precision-Recall曲线](https://zhuanlan.zhihu.com/p/476700983)。用法示例如下所示：

```python3
 1 def add_pr_curve(writer):
 2     from sklearn.linear_model import LogisticRegression
 3     from sklearn.preprocessing import label_binarize
 4     def get_dataset():
 5         from sklearn.datasets import load_iris
 6         from sklearn.model_selection import train_test_split
 7         x, y = load_iris(return_X_y=True)
 8         random_state = np.random.RandomState(2020)
 9         n_samples, n_features = x.shape
10         # 为数据增加噪音维度以便更好观察pr曲线
11         x = np.concatenate([x, random_state.randn(n_samples, 100 * n_features)], axis=1)
12         x_train, x_test, y_train, y_test = train_test_split(x, y, test_size=0.5,
13                                                             random_state=random_state)
14         return x_train, x_test, y_train, y_test
15 
16     x_train, x_test, y_train, y_test = get_dataset()
17     model = LogisticRegression(multi_class="ovr")
18     model.fit(x_train, y_train)
19     y_scores = model.predict_proba(x_test)  # shape: (n,3)
20 
21     b_y = label_binarize(y_test, classes=[0, 1, 2])  # shape: (n,3)
22     for i in range(3):
23         writer.add_pr_curve(f"pr_curve/label_{i}", b_y[:, i], y_scores[:, i], global_step=1)
```

在上述代码中，第2-19行代码用来根据逻辑回归生成预测结果，其中第11行用来给原始数据加入噪音，目的是为了可视化得到更加真实的PR曲线；第21行用来将原始标签转化为one-hot编码形式的标签；第22-23行则是分别根据每个类别的预测结果画出对应的PR曲线。运行上述代码将会得到类似如图16所示的结果。

![img](https://pic2.zhimg.com/v2-fb2adc63091693608db9c1a90fbff637_1440w.jpg)

图 16. add_pr_curve可视化结果图

### **3.9 `add_embedding`方法**

这个方法作用是在三维空间中对高维向量进行可视化，默认情况下是对高维向量以PCA方法进行降为处理。`add_embedding()`方法主要有三个比较重要的参数 `mat`、`metadata`和 `label_img`，下面掌柜依次来进行介绍。

`mat`：用来指定可视化结果中每个点的坐标，形状为(N,D)，**不能为空，**例如对词向量可视化时 `mat`就是词向量矩阵，图片分类时 `mat`可以是分类层的输出结果；

`metadata`：用来指定每个点对应的标签信息，是一个包含N个元素的字符串列表，为空时则默认为 `['1','2',....,'N']`;

`label_img`：用来指定每个点对应可视化信息，形状为(N,C,H,W)，可以为空，例如图片分类时 `label_img`就是每一张真实图片的可视化结果。

进一步，我们便可以通过如下代码来进行三维空间的高维向量可视化：

```text
 1 def add_embedding(writer):
 2     import tensorflow as tf
 3     import tensorboard as tb
 4     tf.io.gfile = tb.compat.tensorflow_stub.io.gfile
 5     import keyword
 6     import torch
 7     # 随机生成100个标签信息
 8     meta = []
 9     while len(meta) < 100:
10         meta = meta + keyword.kwlist  # get some strings
11     meta = meta[:100]
12     for i, v in enumerate(meta):
13         meta[i] = v + str(i)
14     # 随机生成100个标签图片
15     label_img = torch.rand(100, 3, 10, 32)
16     for i in range(100):
17         label_img[i] *= i / 100.0
18     data_points = torch.randn(100, 5)  # 随机生成100个点
19     writer.add_embedding(mat=data_points, metadata=meta, label_img=label_img, global_step=1)
```

在上述代码中，第2-4行用于解决TensorFlow1.x版本的兼容性问题；第8-13行则是随机生成100个字符串标签信息；第15-17行则是生成标签对应的图片；第18行则是随机生成需要可视化的高维向量。上述代码运行结束后便会得到如图17所示的结果。

![img](https://picx.zhimg.com/v2-5adf000953e1f992ec548b10979d9139_1440w.jpg)

图 17. add_embedding可视化结果图

如图17所示，字符串就是上面代码中对应的 `metadata`参数，黑色方块就是对应的 `label_img`参数，而方块背后的点（图中看不到）就是对应的 `mat`参数。这里掌柜只是用了随机数据生成了上面这张图，在下一节中掌柜将会用一个实际的例子来进行展示。

## TensorBoard 的使用实例

### **定义模型**

这里，掌柜以LeNet5网络模型进行示例，所以首先需要定义模型的前向传播过程，代码如下：

```python3
 1 import torch.nn as nn
 2 
 3 class LeNet5(nn.Module):
 4     def __init__(self, ):
 5         super(LeNet5, self).__init__()
 6         self.conv = nn.Sequential(  # [n,1,28,28]
 7             nn.Conv2d(1, 6, 5, padding=2),  # in_channels, out_channels, kernel_size
 8             nn.ReLU(),  # [n,6,24,24]
 9             nn.MaxPool2d(2, 2),  # kernel_size, stride  [n,6,14,14]
10             nn.Conv2d(6, 16, 5),  # [n,16,10,10]
11             nn.ReLU(),
12             nn.MaxPool2d(2, 2))  # [n,16,5,5]
13 
14         self.fc = nn.Sequential(
15             nn.Flatten(),
16             nn.Linear(16 * 5 * 5, 120),
17             nn.ReLU(),
18             nn.Linear(120, 84),
19             nn.ReLU(),
20             nn.Linear(84, 10))
21 
22     def forward(self, img, labels=None):
23         output = self.conv(img)
24         logits = self.fc(output)
25         if labels is not None:
26             loss_fct = nn.CrossEntropyLoss(reduction='mean')
27             loss = loss_fct(logits, labels)
28             return loss, logits
29         else:
30             return logits
```

在上述代码中，第25-30行为根据不同的输入情况返回不同的结果。其余部的代码相对较为简单掌柜这里就不再赘述了，可以参考文章**卷积池化与LeNet5网络模型**。

### 定义分类模型

- 数据集构造

首先，我们需要构造训练模型时使用到的数据集，这里掌柜还是以FashionMNIST为例进行示例。构造代码如下所示：

```python3
 1   text_labels = ['t-shirt', 'trouser', 'pullover', 'dress', 'coat',
 2                  'sandal', 'shirt', 'sneaker', 'bag', 'ankle boot']
 3   
 4   def load_dataset(batch_size=64):
 5       mnist_train = torchvision.datasets.FashionMNIST(root='~/Datasets/FashionMNIST',
 6                                                       train=True, download=True,
 7                                                       transform=transforms.ToTensor())
 8       mnist_test = torchvision.datasets.FashionMNIST(root='~/Datasets/FashionMNIST',
 9                                                      train=False, download=True,
10                                                      transform=transforms.ToTensor())
11       train_iter = torch.utils.data.DataLoader(mnist_train,batch_size=batch_size,
12                                                shuffle=True,num_workers=1)
13       test_iter = torch.utils.data.DataLoader(mnist_test,batch_size=batch_size,
14                                               shuffle=True,num_workers=1)
15       return train_iter, test_iter
```

在上述代码中，第1-2行为定义的每个标签序号所对应的标签名，用于在使用 `add_embedding`可视化预测结果时展示每个样本的标签名称；第5-15行则是分别构造训练集和测试集的DataLoader对象。

- 定义分类模型

进一步，我们需要定义一个类来实现模型的整个训练和推理过程。首先定义这个类的初始化方法，代码如下：

```python3
 1   class MyModel:
 2       def __init__(self,
 3                    batch_size=64,
 4                    epochs=3,
 5                    learning_rate=0.01):
 6           self.batch_size = batch_size
 7           self.epochs = epochs
 8           self.learning_rate = learning_rate
 9           self.model_save_path = 'model.pt'
10           self.device = torch.device('cuda:0' if torch.cuda.is_available() else 'cpu')
11           self.model = LeNet5()
```

- 定义评估方法

在这里，我们先定义一个评估函数，用来计算在测试集上模型的准确率。同时返回我们在使用Tensoboard可视化时需要用到的相关变量，代码如下：

```python3
 1       @staticmethod
 2       def evaluate(data_iter, net, device):
 3           net.eval()
 4           all_logits = []
 5           y_labels = []
 6           images = []
 7           with torch.no_grad():
 8               acc_sum, n = 0.0, 0
 9               for x, y in data_iter:
10                   x, y = x.to(device), y.to(device)
11                   logits = net(x)
12                   acc_sum += (logits.argmax(1) == y).float().sum().item()
13                   n += len(y)
14                   all_logits.append(logits)
15                   y_pred = logits.argmax(1).view(-1)
16                   y_labels += (text_labels[i] for i in y_pred)
17                   images.append(x)
18               net.train()
19               return acc_sum / n, torch.cat(all_logits, dim=0), y_labels, torch.cat(images, dim=0)
```

在上述代码中，第1行表示将这个方法声明为静态方法，因为函数里面没有使用到相关类成员；第4-6行分别定义了三个列表用于保存所有样本的预测logits向量、标签文本和原始表示；第10-13行用来累计预测正确样本的个数；第14-17分别用来处理得到在使用 `add_embedding`时所需要用到的变量；第19行则是返回所有需要用到的结果。

- 定义训练过程

在完成上述步骤后便可以来实现模型训练部分的代码，同时对需要可视化的变量进行记录。由于这部分代码较长，掌柜就分块进行介绍。

```python3
 1       def train(self):
 2           train_iter, test_iter = load_dataset(self.batch_size)
 3           last_epoch = -1
 4           if os.path.exists('./model.pt'):
 5               checkpoint = torch.load('./model.pt')
 6               last_epoch = checkpoint['last_epoch']
 7               self.model.load_state_dict(checkpoint['model_state_dict'])
 8   
 9           num_training_steps = len(train_iter) * self.epochs
10           optimizer = torch.optim.Adam([{"params": self.model.parameters(),
11                                          "initial_lr": self.learning_rate}])
12           scheduler = get_cosine_schedule_with_warmup(optimizer, num_warmup_steps=300,
13                                                       num_training_steps=num_training_steps,
14                                                       num_cycles=2, last_epoch=last_epoch)
```

在上述代码中，第4-7行用来判断本地是否存在之前保存的模型，如果存在则直接载入，而 `last_epoch`是用来获取得到之前模型结束训练时的状态，目的是能够使得Tensoboard在可视化的时候能够接着之前的数据集进行可视化（详情可以参见文章[Transformers之自定义学习率动态调整第4节内容](https://zhuanlan.zhihu.com/p/466992867)；第10-14行则是用来分别定义优化器和学习率动态调整策略。

进一步，实现模型的训练步骤可损失、准确率和学习率的可视化过程，代码如下：

```python3
 1           writer = SummaryWriter("runs/nin")
 2           max_test_acc = 0
 3           for epoch in range(self.epochs):
 4               for i, (x, y) in enumerate(train_iter):
 5                   x, y = x.to(self.device), y.to(self.device)
 6                   loss, logits = self.model(x, y)
 7                   optimizer.zero_grad()
 8                   loss.backward()
 9                   optimizer.step()  # 执行梯度下降
10                   scheduler.step()
11                   if i % 50 == 0:
12                       acc = (logits.argmax(1) == y).float().mean()
13                       print("### Epochs [{}/{}]---batch[{}/{}]---acc {:.4}---loss {:.4}".format(
14                           epoch + 1, self.epochs, i, len(train_iter), acc, loss.item()))
15                       writer.add_scalar('Training/Accuracy', acc, scheduler.last_epoch)
16                   writer.add_scalar('Training/Loss', loss.item(), scheduler.last_epoch)
17                   writer.add_scalar('Training/Learning Rate', 
18                                     scheduler.get_last_lr()[0], scheduler.last_epoch)
```

在上述代码中，第1行用来实例化 `SummaryWriter`用于后续可视化操作；第5-14行则是用来执行整个模型的训练过程；第15-18行则是用来分别对训练集上的准确率、损失和学习率进行可视化。

最后一步便是通过 `add_embedding`来对预测结果进行可视化，代码如下：

```python3
1               test_acc, all_logits, y_labels, label_img = self.evaluate(test_iter, 
2                                                                         self.model, self.device)
3               writer.add_scalar('Testing/Accuracy', test_acc, scheduler.last_epoch)
4               writer.add_embedding(mat=all_logits,  # 所有点
5                                    metadata=y_labels,  # 标签名称
6                                    label_img=label_img,  # 标签图片
7                                    global_step=scheduler.last_epoch)
```

在上述代码中，第1-2行主要用来获取 `add_embedding`所需要的遍历；第3-7行则是分别对测试集上的准确率和预测结果进行可视化。

### **可视化展示**

在完成所有部分的编码工作后，便可以通过如下代码来运行整个模型：

```python3
1 if __name__ == '__main__':
2     model = MyModel()
3     model.train()
```

在程序运行开始后，便可以通过第3.1节中的方式启动Tensoboard前端界面，并可以看到如下图所示的可视化结果。

![img](https://picx.zhimg.com/v2-02c38717d41c6954e3c725199afe8205_1440w.jpg)

图 18. LeNet5训练可视化结果图

如图18所示便是模型在训练过程中在训练集上的准确率、学习率和损失的变化结果。

![img](https://pica.zhimg.com/v2-1c03a34a2af42f4280e12a8d8e01662a_1440w.jpg)

图 19. LeNet5模型预测标签可视化结果图（一）

如图19所示便是模型在测试集上的预测结果经过 `add_embedding`方法可视化后的结果，其中每个小方块都表示一个原始样本，每种颜色代表一个类别。进一步，点击任意方块便可以查看该样本的相关信息，如图20所示。

![img](https://pic1.zhimg.com/v2-fee5c2572a02399ca601836a27fd0f92_1440w.jpg)

图 20. LeNet5模型预测标签可视化结果图（二）

如图20所示便是ankle boot的可视化结果，并且可以发现只要点击其中一个样本，与它类别相同的样本也会被标记出来。当然，该页面还有其它相应的功能大家可以试着去探索，这里掌柜就不进行介绍了。

## 参考

> https://blog.csdn.net/qq_32939413/article/details/106008426
