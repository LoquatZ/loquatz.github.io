## 必备软件

### 火绒（Win）

!> Windows 安全防护的软件、功能模块完全解耦、最好用、最干净、最简洁、没有之一 ！
> 下载地址[https://www.huorong.cn/](https://www.huorong.cn/)

---

### Clash For Windows | v2ray
!> Windows 客户端 VPN
>下载地址 Clash：[https://github.com/Fndroid/clash_for_windows_pkg/releases](https://github.com/Fndroid/clash_for_windows_pkg/releases)
>下载地址 v2ray：[https://github.com/v2fly/v2ray-core/tags](https://github.com/v2fly/v2ray-core/tags)

---

### Chrome
!> 谷歌浏览器  搭配 VPN 使用更香哦~
>下载地址：[https://www.google.com/chrome/](https://www.google.com/chrome/)

---

### BandZip (Win)
!> 很好用的一个解压工具 无广告，操作丝滑
>下载地址：[https://www.bandisoft.com/bandizip/](https://www.bandisoft.com/bandizip/)

### Bob (Mac)
!> Mac最好用的翻译软件

>下载地址：[https://github.com/ripperhe/Bob/releases/tag/v0.10.3](https://github.com/ripperhe/Bob/releases/tag/v0.10.3) 免费版已停止更新建议使用正式版
>AppStore:[https://apps.apple.com/cn/app/id1630034110](https://apps.apple.com/cn/app/id1630034110)
## 编译环境

###  Python (Win/Mac)
!> 脚本&后台语言
- **Win 安装**
>下载地址：[https://www.python.org/downloads/](https://www.python.org/downloads/)

- **Mac 安装**

```bash
# 安装
brew install pyenv
```
```bash
# 查看可安装版本
pyenv install -l
```
```bash
# 安装指定版本
pyenv install 3.9.15
```
```bash
# 指定使用版本
pyenv global 3.9.15
```
```bash
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```
---

### Node js & nvm (Win/Mac)
!> 一个基于 Chrome V8 引擎的 JavaScript 运行环境，nvm 为Node js 的包管理工具，可通过nvm指定版本安装Nodejs
- **Win 安装**
>下载地址 NVM：[https://github.com/coreybutler/nvm-windows/releases/](https://github.com/coreybutler/nvm-windows/releases)
>下载地址 Node js：[https://nodejs.org/en/](https://nodejs.org/en/)
- **Mac 安装**
```bash
# 安装 n
brew install n
```
```bash
#查看可用版本
n ls-remote --all
```
```base
sudon install 14.17.6
```

---

### JDK (Win/Mac)
!> Java 编译运行环境
- **Win 安装**
>下载地址：[https://www.oracle.com/java/technologies/downloads/#java8-windows](https://www.oracle.com/java/technologies/downloads/#java8-windows)
- **Mac 安装**
1. 安装虚拟环境
```bash
# 安装
brew install jenv
```
2. 添加环境变量
```bash
export PATH="$HOME/.jenv/bin:$PATH"
eval "$(jenv init -)"
```
2. 下载JDK
> 下载地址：[https://www.oracle.com/java/technologies/downloads/#java8-mac](https://www.oracle.com/java/technologies/downloads/)
3. 添加JDK
安装几个添加几个
```bash
jenv add /Library/Java/JavaVirtualMachines/jdk1.8.0_281.jdk/Contents/Home jdk1.8 added
```
```bash
jenv add /Library/Java/JavaVirtualMachines/jdk11.0.
```bash
# 指定版本使用
jenv global 1.8
```
---

### Git (Win/Mac)
!> 分布式版本控制系统
- **Win 安装**
>下载地址：[https://git-scm.com/](https://git-scm.com/)
- **Mac 安装**
```
brew install git
```
---

### Flutter （Win/Mac）
!> Flutter是Google开源的构建用户界面（UI）工具包
``` git
git clone https://github.com/flutter/flutter.git -b stable
```
- **Win 安装**
```
高级系统设置 -> 环境变量 -> path -> Windows 安装位置
```
>下载地址：[https://docs.flutter.dev/get-started/install/windows](https://docs.flutter.dev/get-started/install/windows)
- **Mac 安装**
```bash
# 设置环境变量
export PATH="$PATH:Flutter安装位置/flutter/bin"
---

### Homebrew (Mac)
!> Mac 包管理工具
```zsh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## 代码工具

### AndroidStudio (Win/Mac)
!> Android ， Flutter 编译器
>下载地址：[https://developer.android.com/studio](https://developer.android.com/studio)

---

### Visual Studio Code (Win/Mac)
!> 好用的编辑器
>下载地址：[https://code.visualstudio.com/](https://code.visualstudio.com/)

---

### Sublime Text 3 (Win/Mac)
!> 轻量编辑器
>下载地址:[https://www.sublimetext.com/3](https://www.sublimetext.com/3)

---

### Apifox (Win/Mac)
!> API 文档,API 调试
>下载地址:[https://www.apifox.cn/](https://www.apifox.cn/)

### Sourcetree (Win/Mac)
!> Git 图形化工具
>下载地支:[https://www.sourcetreeapp.com/](https://www.sourcetreeapp.com/)