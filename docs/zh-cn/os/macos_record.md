## 快捷键

!>Mac OS 默认切换输入法为 `Ctrl+space ` 和 `ctrl+option+space`

因为大多编译器的默认输入提示的快捷键都为 `ctrl+space` 所以需要关掉

```
系统偏好设置:
          -> 键盘
            -> 快捷键
              -> 输入法
                -> （取消勾选）选择上一个输入法
```



---



## 终端Shell

!> Mac OS 常用的终端Shell有 `bash` 和  `zsh`

### 使用命令查看系统中可用的shell

```bash
cat /etc/shells
```

> 输出以下内容

```
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

### 使用 `chsh` 命令切换Shell

```bash
# 切换 Shell 至 ZSH
chsh -s /bin/zsh
# 切换 Shell 至 BASH
chsh -s /bin/bash
```

!> 从 Mac OS Catalina 版本开始，使用了 `zsh` 作为默认的Shell指令

### Shell对应的配置文件

|   zsh    |      bash       |
| :------: | :-------------: |
| ~/.zshrc | ~/.bash_profile |

`~/`代表用户目录，例如你的用户名为 `loquatz` 则 你的完整用户目录为 `/Users/loquatz`

!>如果你是从 `bash` 转到 `zsh` 的用户，需要将 `bash` 文件同步到 `.zshrc` 中，反之同理。

```bash
# zsh用户
source ~/.bash_profile

# bash用户
source ~/.zshrc
```

!>最好将`配置` 写到一个`shell配置文件`中，方便管理，`zsh` 完全兼容 `bash`，所以可以只使用一个`zsh`就足够了，这也是`Mac`将，`shell`切换成`zsh`的主要原因

### 快速同步修改后的shell文件

如果刚修改过 `shell` 配置文件，可通过 `source` 命令，快速生效。

```bash
# zsh用户
source .zshrc

# bash用户
source .bash_profile
```

