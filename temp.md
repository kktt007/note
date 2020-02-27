## windows 安装SF 字体
[下载安装字体](https://developerjillur.me/san-francisco-font-download/)
个性化设置，找到字体，或者
cmd+R fonts找到字体
SF Pro Text
vscode字体: 
"editor.fontFamily": "'MesloLGM Nerd Font Mono', 'FiraCode Nerd Font Mono', 'SF Pro Text', 'Droid Sans Mono', 'monospace', monospace, '全字庫正楷體', '文泉驿微米黑', '楷体'",
chenxi配置:

https://github.com/login/oauth/authorize?scope=gist read:user&client_id=cfd96460d8b110e2351b&redirect_uri=http://localhost:54321/callback

9facf3a8dc15812395e73cf8eca618e57f3a58c0

# **[cloudSettings](https://gist.github.com/kktt007/47df1b995cfa27cb4da5587513ed0a50)**

[To solve it I did the following](https://github.com/shanalikhan/code-settings-sync/issues/321)
我做的第二步，然后他自己生成了token,验证了本地客户端(# Success! You may now close this tab.)，然后找几个gist不用的，重新传
1.  regenerate the token
2.  reset settings + delete all the lines in settings.json with sync.*
3.  restarted VS Code
4.  upload settings

3f1816525ce73d6005a4ea0fb91801167474c082

linux:
e91647653ad84531e49495dfc4d63d3a
ef6c250744fcacef3d44b7059b7a3f566a671e


46fef847fa9fa0f847ea6d79cedbab33e84c795a
6715df07ec5cf0a9f206ba476553815ac5699dba
c975ab928093d88cffbbc654e3393c1ffdc58fe3


08e5b46069b4332a5da444748b598a5dc678a010
b1b333e2de4bac7b666e73ce0ebe97e1a72061ce

3b3c0f49b3297b70cb7bb01734c8cb3023d49e96
老的
edfe6341d5cba049c497c4b382da1dc0

3326862fdc75e118310c78a9a7685507963c54f3

一直以为查单词，查字典就行了，原来修行如此重要，因为字典也有根源，字典的起源怎么来的。美国传统词典The American Heritage dictionary 的标准，音标等等，有何意义

## 创建gist token
https://myzerone.com/posts/2017/12/14/atom同步/
https://www.cnblogs.com/lychee/p/11214032.html
https://help.github.com/cn/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line
https://cloud.ibm.com/docs/services/ghededicated?topic=ghededicated-getting-started

## i3 with plasma
https://github.com/avivace/dotfiles
https://wiki.archlinux.org/index.php/KDE#Use_a_different_window_manager
https://github.com/nightsh/i3-plasma
https://github.com/heckelson/i3-and-kde-plasma
https://userbase.kde.org/Tutorials/Using_Other_Window_Managers_with_Plasma
https://ryanlue.com/posts/2019-06-13-kde-i3
https://medium.com/@vishnu_mad/using-i3-window-manager-with-kde-plasma-c2ac70594d8
https://www.reddit.com/r/unixporn/comments/64mihc/i3_kde_plasma_a_match_made_in_heaven/

## kde

### plasma[kde和gtk的theme/icon分别设置)](https://i.redd.it/k23gf0rfuow11.png)

```
确保开启了: 
1.Settings > Display and Monitor > Compositor
Check "Enable compositor on startup"
```
[参考kde](https://userbase.kde.org/Tutorials/Force_Transparency_And_Blur)
- icons: [Papirus icon theme](https://github.com/PapirusDevelopmentTeam/papirus-icon-theme)
- font: monaco
- wm: [i3](https://i.redd.it/rprzkxe7cl331.jpg)
- window decoration
- look and feel: Work in progress
- dock: latte dock
- global theme: [kde上使用的gtk-- Materia KDE](https://github.com/PapirusDevelopmentTeam/materia-kde)
- plasma theme
- kvantum:
	- engine: [kvantum](https://github.com/tsujan/Kvantum/tree/master/Kvantum)
	- theme: [Kv Glass](https://store.kde.org/p/1201321/ "KvGlassManjaro.tar.gz")
- wedjet:
	- global menu, windows button, window list(latte task), application launcher,system tray.
1. blur light strength [设置百分比参考2/3](https://imgur.com/gallery/T9htiB1),最强也可以
2. background transparency设置1/3




## KDE blur
https://www.reddit.com/r/unixporn/comments/9un99u/kde_plasma_do_you_need_so_more_blur/?utm_source=share&utm_medium=web2x

https://www.reddit.com/r/kde/comments/ekiw85/dark_breeze_blur_simple_kde_top_bar/

Kvantum:
In KDE:
Select Kvantum from System Settings → Application Style → Widget Style and apply it.
Select Kvantum from System Settings → Color → Scheme and click Apply.
papirus-icon-theme 需要安装 yay hardcode-fixer-git papirus-folders-git(使用方法:https://github.com/PapirusDevelopmentTeam/papirus-folders#script-usage)


Global Menu(key words):
Windows Decoration
Application Menu icon
Widget Style
Title bar button
```
Kvantum Manager → Configure Active Theme → Compositing & General Look → Blurring for menus and tooltips.
```
_Appearance → Application Style"_ , you must select kvantum
kvantum 是一个引擎，需要在安装主题
[kvantum theme](https://store.kde.org/browse/cat/123/ord/rating/)

[kde port](https://www.reddit.com/r/kde/comments/a9s1u4/list_of_themes_ported_to_both_qt_and_gtk/)

### Script usage

Papirus-folders doesn't have a GUI, but it is a fully functional command-line application with TAB-completions. Below you'll see some examples of use.

#### [](https://github.com/PapirusDevelopmentTeam/papirus-folders#show-the-current-color-and-available-colors-for-papirus-dark)Show the current color and available colors for Papirus-Dark

```
papirus-folders -l --theme Papirus-Dark

```

#### [](https://github.com/PapirusDevelopmentTeam/papirus-folders#change-color-of-folders-to-brown-for-papirus-dark)Change color of folders to brown for Papirus-Dark

```
papirus-folders -C brown --theme Papirus-Dark

```

#### [](https://github.com/PapirusDevelopmentTeam/papirus-folders#revert-to-default-color-of-folders-for-papirus-dark)Revert to default color of folders for Papirus-Dark

```
papirus-folders -D --theme Papirus-Dark

```

#### [](https://github.com/PapirusDevelopmentTeam/papirus-folders#restore-the-last-used-color-from-a-config-file)Restore the last used color from a config file

```
papirus-folders -Ru
```
-----

vs code plugin

Visual Studio Intellicode

Path Intellisense

Settings Sync

Bracket Pair Colorizer

Markdown All in One (prview:ctrl+shift+v, preview to side:ctrl+k +v)

GitHub Extension

Code Spell Checker

Better Comments

Fira Code

Prettier

Regex Previewer

vscode-icons

EditorConfig for VS Code

Server = http://mirrors.aliyun.com/archlinux/$repo/os/$arch
Server = http://mirrors.163.com/archlinux/$repo/os/$arch
Server = https://mirrors.huaweicloud.com/archlinux/$repo/os/$arch

[archlinuxcn]
Server = http://mirrors.163.com/archlinux-cn/$arch
Server = https://mirrors.cloud.tencent.com/archlinuxcn/$arch

gitlens
------
---------
### bash
> https://www.gnu.org/software/bash/


>  [Bash builtinsBuilt in Bash commands](https://helpmanual.io/builtin/)

>

> https://ss64.com/bash/

>

> https://www.tldp.org/LDP/Bash-Beginners-Guide/html/Bash-Beginners-Guide.html

>

> https://gerardnico.com/lang/bash/builtin

>

>https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins.html

> https://www.gnu.org/software/bash/manual/html_node/Builtin-Index.html#Builtin-Index

>

> https://www.gnu.org/software/bash/manual/html_node/index.html

>

> http://man7.org/linux/man-pages/man1/set.1p.html

>

>  [Special Built-in Utilities](https://pubs.opengroup.org/onlinepubs/009695399/idx/sbi.html)

>

> https://en.wikibooks.org/wiki/Bash_Shell_Scripting

>

> https://github.com/LeCoupa/awesome-cheatsheets/blob/master/languages/bash.sh

>

> http://manpages.ubuntu.com/manpages/bionic/man7/bash-builtins.7.html#bash builtin commands
> 

v2ray配置
```
{
  "policy": null,
  "log": {
    "access": "",
    "error": "",
    "loglevel": "warning"
  },
  "inbounds": [
    {
      "tag": "proxy",
      "port": 10808,
      "listen": "127.0.0.1",
      "protocol": "socks",	//入站协议
      "sniffing": {
        "enabled": true,
        "destOverride": [
          "http",
          "tls"
        ]
      },
      "settings": {
        "auth": "noauth",	//不认证
        "udp": true,
        "ip": null,
        "address": null,
        "clients": null
      },
      "streamSettings": null
    }
  ],
  "outbounds": [
    {
      "tag": "proxy",
      "protocol": "vmess",	//出口协议
      "settings": {
        "vnext": [
          {
            "address": "whcu.988998.xyz",
            "port": 80,	服务器端口
            "users": [
              {
                "id": "4D003F3B-DECC-6C89-BADB-43156C0E1CEF",
                "alterId": 0,
                "email": "t@t.tt",
                "security": "auto"
              }
            ]
          }
        ],
        "servers": null,
        "response": null
      },
      "streamSettings": {
        "network": "ws",
        "security": null,
        "tlsSettings": null,
        "tcpSettings": null,
        "kcpSettings": null,
        "wsSettings": {
          "connectionReuse": true,
          "path": null,
          "headers": {
            "Host": "itunes.apple.com.ajax.microsoft.com.www.bing.com.hkta.xianexpress.com.cn"
          }
        },
        "httpSettings": null,
        "quicSettings": null
      },
      "mux": {
        "enabled": true
      }
    },
    {
      "tag": "direct",
      "protocol": "freedom",
      "settings": {
        "vnext": null,
        "servers": null,
        "response": null
      },
      "streamSettings": null,
      "mux": null
    },
    {
      "tag": "block",
      "protocol": "blackhole",
      "settings": {
        "vnext": null,
        "servers": null,
        "response": {
          "type": "http"
        }
      },
      "streamSettings": null,
      "mux": null
    }
  ],
  "stats": null,
  "api": null,
  "dns": null,
  "routing": {
    "domainStrategy": "IPIfNonMatch",
    "rules": [
      {
        "type": "field",
        "port": null,
        "inboundTag": [
          "api"
        ],
        "outboundTag": "api",
        "ip": null,
        "domain": null
      }
    ]
  }
}
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbODU1MTgzNzYwLC00NzkwNjk5NzIsMTY2Nz
E3MTIxNiwxNTA0MDI0MzMsMTczMDc4NjI0NCwxMjkyNjc2Mjcy
LC0xNzU3MjMzMDM4LDE0ODMxNTk2ODAsMTAyODgzMDgyMiwxMj
M1MDExNDU1LC02NTEyMDcsMTUyMjY2OTU4MSwtMTgzMzc3Nzc0
MCw4MzAzNDY0ODgsMTc3OTg4MDE4MywtMjU0MDcyMjI4LC0xNj
gzNDg1MDUzLC0xMjI5MzQ4NjA1LDI5OTY1MzU5MiwtMTk1OTkz
MjM4OV19
-->