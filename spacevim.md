
windows: mklink /D %USERPROFILE%\AppData\Local\nvnvim %USERPROFILE%\.SpaceVim
https://github.com/Gabirel/Hack-SpaceVim/blob/master/en_US/installation/installation-for-windows.md#start-to-install
默认的 `<Leader>` 是 \

标签栏上每一个 Tab 或者 Buffer 可通过快捷键 <Leader> number 进行快速访问 
    
```
<Alt> + num 也可以，但只用于Neovim
```
    
窗口管理器快捷键只可以在 Normal 模式下使用，默认的前缀（`WIN`）按键为 `s`，可以在配置文件中通过修改 SpaceVim 选项 `window_leader` 的值来设为其它按键

```
[options]
    windows_leader = "s"
```
Normal 模式下的按键 q 被用来快速关闭窗口，其原生的功能可以使用 <Leader> q r 来代替。

b 为 buffer 相关快捷键前缀

p 为 project 相关快捷键前缀

s 为 search 相关快捷键前缀

h 为 help 相关快捷键前缀

f 为文件操作相关前缀
`SPC f s` 保存文件

`SPC f S` 保存所有文件

`<F3>`  /  `SPC f t` 切换文件树

t/T 界面元素 theme

SPC ? 
使用 Unite 将当前快捷键罗列出来。然后可以输入快捷键按键字母或者描述，Unite 可以模糊匹配并展示结果。

默认主题 gruvbox 的状态栏颜色和模式对照表：

| 模式    | 颜色   |
| :------ | :----- |
| Normal  | 灰色   |
| Insert  | 蓝色   |
| Visual  | 橙色   |
| Replace | 浅绿色 |

| `SPC [1-9]` | 跳至指定序号的窗口 |
| ----------- | ------------------ |

功能模块可以通过 SPC t m m 快捷键显示或者隐藏

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNTM1OTI4MzEsLTI3ODYxNjgwMywyMD
YxMjE2NDQ5LDczMDk5ODExNl19
-->
