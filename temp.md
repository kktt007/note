## 创建gist token
https://myzerone.com/posts/2017/12/14/atom同步/
https://www.cnblogs.com/lychee/p/11214032.html
https://help.github.com/cn/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line
https://cloud.ibm.com/docs/services/ghededicated?topic=ghededicated-getting-started


## kde

### plasma[kde和gtk的theme/icon分别设置)](https://i.redd.it/k23gf0rfuow11.png)
- icons: papirus
- font: monaco
- wm: [i3](https://i.redd.it/rprzkxe7cl331.jpg)
- window decoration
- look and feel: Work in progress
- dock: latte dock
- global theme
- plasma theme
- kvantum:
	- engine:
	- theme: [Kv Glass](https://store.kde.org/p/1201321/ "KvGlassManjaro.tar.gz")
- wedjet:
	- global menu, windows button, window list(latte task), application launcher,system tray.
1. blur light strength [设置百分比参考2/3](https://imgur.com/gallery/T9htiB1)
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
eyJoaXN0b3J5IjpbLTE0NjY4ODA3MTksNzEwNTEzMDkxLDIwMz
cyMzY2NTIsLTEzNzY3MjQ0OCwtMTI5MzA0MzA4OSwtMjE0NTc2
NDA0MywxODg2NDI0NDU0LDE3ODkxNDM3ODAsMTkyMjkwNTY3NS
wxODAwMzg0MDQxLDQ3NDM5MDE5MiwtMTk1NTQ4MTcxNiwxMzE2
MDIxMjMxLC0zODAxMzY1OTAsMTgwMjE5MTQ0OCwtMzA5NjI2Mj
c4XX0=
-->