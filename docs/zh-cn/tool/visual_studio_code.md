## Visula Studio Code

### 必备插件

#### Chinese (Simplified) (简体中文) Language Pack for Visual

> 适用于 VS Code 的中文（简体）语言包

#### Material Icon Theme

> MD风格文件Icon

#### One Dark Theme

> 非常好看的主题

#### Comment Translate

> VSCode 注释翻译

#### Path Intellisense

> 路径自动提示

#### Remote - SSH

> 服务器直连，可以直接将服务器作为开发环境直接操作代码

#### Svg Preview

> SVG 文件快速预览



### 配置文件

1.快捷键打开配置

```
Mac: cmod + shift + p

Win: ctrl + shift + p
```

2.打开配置文件

```
> Open User Settings (JSON)
```

3.配置文件

```json
{
    "editor.fontLigatures": false,
    // 控制折行的方式。
    "editor.wordWrap": "off",
    // 启用后，将在保存文件时删除行尾的空格。
    "files.trimTrailingWhitespace": true,
    "editor.fontWeight": "500",
    // 控制光标样式
    "editor.cursorStyle": "line",
    // 设置为 line 时，控制光标的宽度。
    "editor.cursorWidth": 3,
    // 控制光标的动画样式。
    "editor.cursorBlinking": "smooth",
    "editor.suggestSelection": "first",
    "vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue",
    // 指定工作台中使用的文件图标主题
    "workbench.iconTheme": "material-icon-theme",
    // 在没有从上一会话中恢复出信息的情况下，控制启动时显示的编辑器。
    "workbench.startupEditor": "newUntitledFile",
    // 关闭扩展建议
    // "extensions.ignoreRecommendations": true,
    // 控制在资源管理器内拖放移动文件或文件夹时是否进行确认。
    "explorer.confirmDragAndDrop": false,
    // 控制资源管理器是否在把文件删除到废纸篓时进行确认。
    "explorer.confirmDelete": false,


    // 控制是否在编辑器中自动显示内联建议
    "editor.inlineSuggest.enabled": true,
    // 代码保存
    "editor.codeActionsOnSave": {
        "source.fixAll": true // 自动修复 all
    },
    //折叠配置文件
    "explorer.fileNesting.enabled": true,
    "explorer.fileNesting.patterns": {
        "pubspec.yaml": ".packages, pubspec.lock, .flutter-plugins, .flutter-plugins-dependencies, .metadata, analysis_options.yaml, dartdoc_options.yaml"
    },

    // 控制具有未保存更改的编辑器的
    "files.autoSave": "afterDelay",
    // 主题设置
    "workbench.colorTheme": "One Dark",
    "editor.guides.bracketPairs": true,
    //控制资源管理器是否在打开文件时自动显示并选择。
    "explorer.autoReveal": false,

    // 配置在同步时要忽略的设置。
    "settingsSync.ignoredSettings": [
        // 字体大小
        "editor.fontSize",
        // 终端字体
        "terminal.integrated.fontFamily"
    ],
}
```

4. 安装`code`命令

```
快捷键: cmod + shift + p
输入: >install code
回车安装
```

> 可在终端的任意位置 `code` 文件夹/文件 通过 VsCode直接打开

### 登录账号开启同步

> 登录账号开启同步VSCode会自动同步所有配置以及插件至PC `非常的方便` 
