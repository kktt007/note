## KDE blur
https://www.reddit.com/r/unixporn/comments/9un99u/kde_plasma_do_you_need_so_more_blur/?utm_source=share&utm_medium=web2x

https://www.reddit.com/r/kde/comments/ekiw85/dark_breeze_blur_simple_kde_top_bar/

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

>

>  [Bash builtinsBuilt in Bash commands](https://helpmanual.io/builtin/)

>

> https://ss64.com/bash/

>

> https://www.tldp.org/LDP/Bash-Beginners-Guide/html/Bash-Beginners-Guide.html

>

> https://gerardnico.com/lang/bash/builtin

>

> https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins.html

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
eyJoaXN0b3J5IjpbNDc0MzkwMTkyLC0xOTU1NDgxNzE2LDEzMT
YwMjEyMzEsLTM4MDEzNjU5MCwxODAyMTkxNDQ4LC0zMDk2MjYy
NzhdfQ==
-->