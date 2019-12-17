
默认的 <Leader> 是 \

标签栏上每一个 Tab 或者 Buffer 可通过快捷键 <Leader> number 进行快速访问 

<Alt> + num 也可以，但只用于Neovim

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

t/T 界面元素

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
eyJoaXN0b3J5IjpbMjA2MTIxNjQ0OSw3MzA5OTgxMTZdfQ==
-->