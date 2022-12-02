?>🧰 `iTerm2配置` 使命令行更高效

### iTerm2 介绍

是一款完全免费的，专为 Mac OS 用户打造的命令行应用。直接在[官网](http://iterm2.com),下载并安装即可。

### 设置默认终端

>左上角菜单 iTerm2 -> Make iTerm2 Default Term

### 基础配置

#### 安装 oh-my-zsh

查看系统有几个shell

```bash
cat /etc/shells
```

>显示

```bash
# List of acceptable shells for chpass(1).
# Ftpd will not allow users to connect who are not using
# one of these shells.

/bin/bash
/bin/csh
/bin/dash
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
```

bash是mac中terminal自带的shell，把它换成zsh，这个的功能要多得多。拥有语法高亮，命令行tab补全，自动提示符，显示Git仓库状态等功能。

使用下面命令设置默认shell

```bash
chsh -s /bin/zsh
```

#### 安装oh-my-zsh

git地址:[https://github.com/robbyrussell/oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)

使用 crul 安装：

```bash
#GitHub源(有科学上网推荐使用)
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
```bash
#GitLab源(无科学上网推荐使用)
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

#### 主题

安装成功后，用vim ~/.zshrc打开隐藏文件，修改主题为`cypher`（根据自己喜好决定）
    主题在 ~/.oh-my-zsh/themes/ 下

```bash
ZSH_THEME="cypher"
```

#### 自动提示命令

当我们输入命令时，终端会自动提示你接下来可能要输入的命令，这时按 → 便可输出这些命令，非常方便。

设置如下：

1.克隆仓库到本地 ~/.oh-my-zsh/custom/plugins 路径下

```zsh
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

2.用 vim  ~/.zshrc 打开文件，下滑找到插件设置命令，默认是 plugins=(git) ，我们把它修改为

```zsh
plugins=(zsh-autosuggestions git)
```

3.重新打开终端窗口。

#### 语法高亮

1.克隆仓库到本地 ~/.oh-my-zsh/custom/plugins 路径下

```zsh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```

2.用 vim  ~/.zshrc 打开文件，下滑找到插件设置命令，默认是 plugins=(git) ，我们把它修改为

```zsh
plugins=(
    zsh-autosuggestions
    git
    zsh-syntax-highlighting
)
```

#### Vimrc安装

1.从git上克隆vimrc到 `~/.vim_runtime`文件夹

```zsh
git clone --depth=1 https://github.com/amix/vimrc.git ~/.vim_runtime
```

2.执行脚本

```zsh
sh ~/.vim_runtime/install_awesome_vimrc.sh
```

> 执行成功显示：Installed the Ultimate Vim configuration successfully! Enjoy :-)

#### 添加on-my-zsh自带插件

用 vim  ~/.zshrc 打开文件，下滑找到插件设置命令，默认是 plugins=(git)

```zsh
plugins=(
    zsh-autosuggestions
    git
    zsh-syntax-highlighting
    sublime
    web-search
    z
    adb
    vi-mode
)
```

> 前往 ~/.oh-my-zsh/plugins 查找你需要的插件加入即可 ，也可以去github上搜索插件

#### 永久设置代理（科学上网）
1. 打开.zshrc
```bash
vim .zshrc
```
2. 添加如下内容，端口号取决于你的代理软件，ClashX的默认端口号是7890
```bash
# 添加如下内容
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890 no_proxy=localhost,127.0.0.1,::1
```


#### 界面美观设置（根据自己的喜好而定）
1. comd + , 打开设置
2. 设置属性
```
Appearance -> General
                        -> Theme:Minimal
                        -> Status bar locaiton:Bottom

Profiles
        -> Transparency:20
        -> Blur:20 并打钩
        -> Text -> Font:14
        -> Window -> Columns:120
                  -> Rows:40
        -> Session -> Status bar enabled:打钩
                   -> Configure Status Bar 选择要显示的小部件
                        -> Auto-Rainbow:Light Colors

```