+++
author = "Ping Hu"
categories = ["Terminal", "powerline"]
date = "2016-06-11"
description = "Set up Terminal with zsh, tmux, vim and powerline"
featured = "deskscreen.png"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "Set up Terminal with zsh, tmux, vim and powerline"
type = "post"

+++

效果图如上

# 1. Install zsh

- Check if zsh is already installed on your Linux:

```
$ which zsh
/bin/zsh
```

If you get an output (like I got), it means zsh already exists on your OS. If not, feel free to install it.

- Download and install zsh

```
$ sudo yum install zsh
```

- To simple use zsh, type zsh in your terminal

```
$ zsh
```

# 2. Install tmux

```
yum install tmux 
brew install tmux

# if want to use tmux 2.1 on linux, check below gist
https://gist.github.com/hiddenpower1/cd1d6610680a6d3d8ec96e0572c55813
```

# 3. Install powerline & powerline fonts

安装前确定自己的电脑上已经有大于2.7版本的python

- 通过 pip 安装powerline


```
pip install powerline-status
```

执行pip show powerline-status后你会看到这些

```
Metadata-Version: 1.1
Name: powerline-status
Version: 2.3
Summary: The ultimate statusline/prompt utility.
Home-page: https://github.com/powerline/powerline
Author: Kim Silkebaekken
Author-email: kim.silkebaekken+vim@gmail.com
License: MIT
Location: /Library/Python/2.7/site-packages
Requires: 
```
记下上面的Location备用

- 安装Powerline专用字体

执行完上面两步后，不出意外powerline就已经开始工作了。但是你会发现Bash提示符是一些非常恶心的符号。  出现这样情况的原因是powerline为了美观自己造了一些符号，而这些符号不在Unicode字库内. 所以想要powerline正常显示的话，需要安装特殊处理过的字体。好在有一位热心人的帮助，他把大部分的程序猿常用的等宽字体都打上了powerline patch使得我们的这部配置将异常简单。首先我们从github上下载并安装字体：

```
git clone https://github.com/powerline/fonts.git
cd fonts
./install.sh
```
安装完成后我们就可以在iTerm2或者Terminal的字体选项里看到并选择多个xxx for powerline的字体了。
*注意：对于ASCII fonts和non-ASCII fonts都需要选择for powerline的字体。

# 4. Install oh-my-zsh & plugins

- Install oh-my-zsh 

via curl

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

When the installation is done, edit ~/.zshrc and set ZSH_THEME="agnoster"

- Install zsh-autosuggestions

```
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

Edit ~/.zshrc and replace line plugins=(git) with plugins=(git zsh-autosuggestions)

Create a file ~/.oh-my-zsh/custom/colors.zsh containing ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=240'

- Install zsh-syntax-highlighting

```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

# or on mac:
brew install zsh-syntax-highlighting
```
~~Edit ~/.zshrc and replace line plugins=(git zsh-autosuggestions) with plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
Note: This works for me on Mac but not on redhat linux, got error(TODO)~~

After installation through homebrew, add

```
source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```
to the end of your .zshrc file. After that, it's best to restart your terminal. Sourcing your ~/.zshrc does not seem to work well with this plugin.

- Shorter prompt style

By default, your prompt will now show “user@hostname” in the prompt. This will make your prompt rather bloated. Optionally set DEFAULT_USER in ~/.zshrc to your regular username (these must match) to hide the “user@hostname” info when you’re logged in as yourself on your local machine. You can check your username value by executing whoami in the terminal.

# 5. 配置Bash 使用powerline

配置方法很简单，只需要在Bash配置文件(例如：/etc/bashrc，~/.bashrc)中增加一行代码以调用安装路径下的bindings/bash/powerline.sh 。这样每次生成新的Bash窗口时，都会自动执行powerline.sh文件中的内容。下面以~/.bashrc为例，使用文本编辑软件打开~/.bashrc，在最后添加下面一行代码：

``` 
. /Library/Python/2.7/site-packages/powerline/bindings/bash/powerline.sh
```

*Note: for iTerm2 add this line to ~/.bash_profile, since iTerm2 doesn't read ~/.bashrc
+++
author = "Ping Hu"
categories = ["terminal"]
date = "2016-06-11"
description = "Setup Terminal with zsh, tmux, vim and powerline"
featured = "pic01.jpg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "Setup Terminal with zsh, tmux, vim and powerline"
type = "post"

+++

# 6. 配置tmux 使用powerline

默认的tmux风格比较朴素甚至有些丑陋。如果希望做一些美化和个性化配置的话，建议使用gpakosz的tmux配置。它的本质是一个tmux配置文件，实现了以下功能：

- 基于powerline的美化
- 显示笔记本电池电量
- 和Mac互通的剪切板
- 和vim更相近的快捷键
- 安装方式也很简单如下

```
$ cd
$ rm -rf .tmux
$ git clone https://github.com/gpakosz/.tmux.git
$ ln -s .tmux/.tmux.conf
$ cp .tmux/.tmux.conf.local .
```

# 7. 配置 Vim
I like to use below setting:

https://github.com/amix/vimrc

```
git clone https://github.com/amix/vimrc.git ~/.vim_runtime
sh ~/.vim_runtime/install_awesome_vimrc.sh
```
