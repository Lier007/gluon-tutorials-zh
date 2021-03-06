# 安装和使用

【注意】本节目前只在Linux和macOS下测试过，Windows版本还在测试中。

## 安装需求

每个教程是一个可以编辑和运行的Jupyter notebook。运行这些教程需要`Python`，`Jupyter`和其插件`notedown`，以及最新版`MXNet`。安装这些依赖最方便的是通过conda。

## 通过Conda安装

首先根据操作系统下载并安装[Miniconda](https://conda.io/miniconda.html)。然后安装所需的依赖包并激活环境：

```bash
git clone https://github.com/mli/gluon-tutorials-zh
cd gluon-tutorials-zh
conda env create -f environment.yml
source activate gluon
```

## 运行

运行Jupyter并加载notedown插件：

```bash
jupyter notebook --NotebookApp.contents_manager_class='notedown.NotedownContentsManager'
```

这时候我们可以通过浏览器打开 [http://localhost:8888](http://localhost:8888) 来查看和运行各个教程了。

## 高级选项

### 使用GPU

默认安装的MXNet只支持CPU。有一些教程需要GPU来运行。假设CUDA 7.5或者8.0已经安装了，那么先卸载CPU版本

```bash
pip uninstall mxnet
```

然后选择安装下面版本之一：

```bash
pip install --pre mxnet-cu75 # CUDA 7.5
pip install --pre mxnet-cu80 # CUDA 8.0
```

### 默认开启notedown插件

首先生成jupyter配置文件（如果已经生成过可以跳过）

```bash
jupyter notebook --generate-config
```

将下面这一行加入到生成的配置文件的末尾（Linux/macOS一般在`~/.jupyter/jupyter_notebook_config.py`)

```bash
c.NotebookApp.contents_manager_class = 'notedown.NotedownContentsManager'
```

之后就只需要运行`jupyter notebook`即可。

### 在远端服务器上运行Jupyter

Jupyter的一个常用做法是在远端服务器上运行，然后通过 `http://myserver:8888`来访问。

有时候防火墙阻挡了直接访问对应的端口，但ssh是可以的。如果本地机器是linux或者mac（windows通过第三方软件例如putty应该也能支持），那么可以使用端口映射

```bash
ssh myserver -L 8888:localhost:8888
```

然后我们可以使用[http://localhost:8888](http://localhost:8888)打开远端的Jupyter。

### 运行计时

我们可以通过ExecutionTime插件来对每个cell的运行计时。

```bash
pip install -e jupyter_contrib_nbextensions
jupyter contrib nbextension install --user
jupyter nbextension enable execute_time/ExecuteTime
```
