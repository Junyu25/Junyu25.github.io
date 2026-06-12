---
layout: post
title: "Jupyter Lab服务器端配置"
date: 2019-04-07
description: ""
tags: CS DIY
redirect_from:
  - /posts/ed092bf8/
---

尝试过Jupyter Lab后，其成为了我最喜欢的IDE。然而在本地使用Anaconda自带的Jupyter略显臃肿，也为了不占用仅有的内存，所以将其配置到服务器上，最终可通过浏览器直接访问。期间踩了些许坑，便记录在此。

## 步骤

#### 1 生成jupyter\_notebook\_config.py配置文件

通过命令`jupyter notebook --generate-config`生成配置文件。  
记录下生成的配置文件位置，例如：`/home/.jupyter/jupyter_notebook_config.py`

#### 2.设置访问密码

```shell
jupyter notebook password
Enter password:  ****
Verify password: ****
```

密码会以hash自动写入到`/Users/you/.jupyter/jupyter_notebook_config.json`文件中。

#### 3.编辑配置文件

将配置文件改为如下设置：

```shell
c = get_config()
# Kernel config
c.IPKernelApp.pylab = 'inline'
# Notebook config
c.NotebookApp.ip='*'
c.NotebookApp.open_browser = False
c.NotebookApp.port = 8888  #设置端口号，我这里设置的是8888，可以设置成任意喜欢的
```

其后运行`Jupyter Lab`发现并不能支持外部访问  
尝试在 `~/.jupyter/jupyter_notebook_config.json` 中写入如下内容，尤其是 `"ip": "0.0.0.0"`，这样让服务器监听所有 ip：

```json
{
  "NotebookApp": {
    "ip": "0.0.0.0", 
    "open_browser": false
  }
}
```

注意在结尾加`,`  
网上一般教程写`"ip": "*"`，而实际无法识别是ipv4或ipv6而报错。

#### 4.运行

`jupyter lab`

## 插件推荐

[Awesome JupyterLab](https://github.com/mauhai/awesome-jupyterlab)

`jupyter labextension install @jupyterlab/toc`

`jupyter labextension install jupyterlab-drawio`

`jupyter labextension install @oriolmirosa/jupyterlab_materialdarker`

`jupyter labextension install @jupyterlab/fasta-extension`

[官方文档](https://jupyter-notebook.readthedocs.io/en/stable/public_server.html)
