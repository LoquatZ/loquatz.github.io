## Windows 小技巧

### 快捷键
!> Windows 以及三方软件，无用快捷键太多，导致使用编译器时，大多都被占用

---

1. **Ctrl + Space** 被占用，并且无论怎么修改，还是会自动恢复
- 解决方案: 打开 **Windows注册表**，修改以下参数值
```
[Win + R 输入 regedit 回车]
HKEY_CURRENT_USER\Control Panel\Input Method\Hot Keys\00000010\Key Modifiers 值修改为 00 00 00 00
HKEY_CURRENT_USER\Control Panel\Input Method\Hot Keys\000000\Virtual Key 值修改为 00 00 00 00
```
>修改之后**重启** 系统即可

---

2. **搜狗输入法**  无用快捷键太多
- 解决方案：右键搜狗输入法图标
```
更多设置 ->  属性设置
	->按键
		中英标点切换：Ctrl + 句号  【关闭】
		全半角切换：Shift + Space 【关闭】
		系统功能快捷键            【关闭】 占用最多的一个
```

