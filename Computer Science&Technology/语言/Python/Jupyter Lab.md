#CS/Python

[在Windows上安装和配置 Jupyter Lab 作为桌面级应用程序教程](https://www.jb51.net/article/185214.htm)

# 安装 Jupyter Lab

如果你安装了 Anaconda，最新版的 Anaconda 自带 Lab，可跳过下面这一步。

`pip install jupyter pip install jupyterlab`

安装完后，简单运行一下，在命令提示符模式下输入：`jupyter lab`

# 配置 Jupyter Lab

## 如何更改默认目录？

默认情况下，**Jupyter Lab** 将 `c:/users/username` 设置为默认目录。 我们可以更改默认目录，以便更容易地管理项目。

### 首先生成配置文件

`Jupyter notebook --generate-config`

这会生成一个配置文件，路径终端会给出。

### 打开配置文件

找到c.NotebookApp.notebook，添上自己想要的默认打开路径。注意反斜杠\\要改为斜杠/。

`c.NotebookApp.notebook_dir = 'Z:/OneDrive/CodingHere'`

## 在 Chrome 应用模式下运行

我们可以使用 chrome 浏览器的应用程序模式将 Jupyter Lab 转换成一个独立的桌面应用程序。 这样可以删除所有不必要的工具栏和用户界面，并给人一种本地应用程序或 IDE 的感觉，体验更流畅！

很简单！打开 Jupyter Lab 的配置文件，在最后面添加一行即可！

注：填的是浏览器 .exe 地址，我用的是 Chrome。

`c.NotebookApp.browser='C:/Program Files(x86)/Google/Chrome/Application/chrome.exe --app=%s'`

## 创建快捷方式

每次都通过命令行来打开 Jupyter Lab 确实麻烦。写个.bat文件就好啦。美观一点可以，可以搞个ICON 什么的。

# 安装插件

Jupyter Lab 插件需要 Node.js 和 npm 的支持。[[Node.js]] 官网下一个 LTS 版本就好了。

`jupyter labextension -h`