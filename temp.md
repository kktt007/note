### 5.5
[vim教程](https://www.w3cschool.cn/vim/c9lbkozt.html)
myspacevim.vim
```
function!  myspacevim#before() abort
  let g:spacevim_default_indent = 4
  au FileType markdown setlocal wrap
  au FileType  json,html setlocal shiftwidth=2 softtabstop=2
endfunction


function!  myspacevim#after() abort

endfunction
```
某人的.vimrc
 echo &formatoptions
`SPC t f`   | 高亮临界列，默认 `max_column` 是第 120 列
textwidth不设置的好，wrap设置默认的类型才有更合理。
```
" 使用vim的modeline来设置当前文件的textwidth,避免输入超过78个字符时自动换行
" 使用:verbose set textwidth?命令可以看到vim默认为vim配置脚本设置了textwidth
" 为78,当输入超过78个字符并按下空格键时会自动换行.将textwidth设成0关闭该功能
"" vim: tw=0 :

" 去掉有关vi一致性模式,避免操作习惯上的局限.
set nocompatible

" 让Backspace键可以往前删除字符.
" Debian系统自带的vim版本会加载一个debian.vim文件,默认已经设置这一项,
" 可以正常使用Backspace键.如果使用自己编译的vim版本,并自行配置.vimrc文件,
" 可能就没有设置这一项,导致Backspace键用不了,或者时灵时不灵.所以主动配置.
set backspace=indent,eol,start

" 1=启动显示状态行, 2=总是显示状态行.设置总是显示状态行,方便看到当前文件名.
set laststatus=2

" 设置ruler会在右下角显示光标所在的行号和列号,不方便查看.改成设置状态栏显示内容
"" set ruler

" 设置状态行显示的内容. %F: 显示当前文件的完整路径. %r: 如果readonly,会显示[RO]
" %B: 显示光标下字符的编码值,十六进制. %l:光标所在的行号. %v:光标所在的虚拟列号.
" %P: 显示当前内容在整个文件中的百分比. %H和%M是strftime()函数的参数,获取时间.
set statusline=%F%r\ [HEX=%B][%l,%v,%P]\ %{strftime(\"%H:%M\")}

" 显示还没有输入完整的命令.例如yy命令,输入第一个y会在右下角显示y.
set showcmd

" 使用Tab键补全时,在状态栏显示匹配的列表,方便查看都有哪些命令符合补全条件.
set wildmenu

" 显示行号
set number

" 高亮显示匹配的括号
set showmatch

" 高亮显示所有搜索到的内容.后面用map映射快捷键来方便关闭当前搜索的高亮.
set hlsearch

" 光标立刻跳转到搜索到内容
set incsearch

" 搜索到最后匹配的位置后,再次搜索不回到第一个匹配处
set nowrapscan

" 去掉输入错误时的提示声音
set noeb

" 默认按下Esc后,需要等待1秒才生效,设置Esc超时时间为100ms,尽快生效
set ttimeout
set ttimeoutlen=100

" 设置文件编码,主要是避免中文乱码.先注释,后续遇到中文乱码再打开
"" set fileencodings=utf-8,cp936,big5,latin1

" FIXME 在MS-DOS控制台打开vim时,控制台使用鼠标右键来复制粘贴,设置
" 全鼠标模式,鼠标右键被映射为visual mode,不能用来复制粘贴,不方便.
" 但是如果不设置鼠标模式,会无法使用鼠标滚轮来滚动界面.经过验证,发现
" 可以设成普通模式mouse=n来使用鼠标滚轮,也能使用鼠标右键复制粘贴.
" mouse=c/mouse=i模式都不能用鼠标滚轮. Linux下还是要设成 mouse=a
set mouse=n

" FIXME 在MS-DOS控制台打开vim,光标很小,不方便看到光标在哪里.下面
" 设置cursorline,高亮光标所在的行.cursorlineopt=number只高亮行号部分,
" 不影响正文内容的显示. 在其他容易看到光标的终端上可以去掉这两个设置.
set cursorline
set cursorlineopt=number

" 开启语法高亮
syntax enable

" 检测文件类型,并载入文件类型插件,为特定文件类型载入相关缩进文件
filetype plugin indent on

" 设置自动补全的选项. longest表示只自动补全最大匹配的部分,剩余部分通过
" CTRL-P/CTRL-N来选择匹配项进行补全. menu表示弹出可补全的内容列表.
" 如果有多个匹配,longest选项不会自动选中并完整补全,要多按一次CTRL-P,比较
" 麻烦,不做设置,保持默认设置,vim默认没有设置longest.
"" set completeopt=longest,menu

" 自动缩进.这个导致从外面拷贝多行以空格开头的内容时,会有多的缩进,先不设置.
"" set autoindent

" 设置C风格的自动缩进.设置filetype indent on后,就会根据文件类型自动缩进.
" 按照vim用户手册'30.3 Automatic indenting'的说明,可以不再单独设置cindent.
"" set cindent

" 自动缩进时,缩进长度为4
set shiftwidth=4

" 输入Tab字符时,自动替换成空格
set expandtab

" 设置softtabstop有一个好处是可以用Backspace键来一次删除4个空格.
" softtabstop的值为负数,会使用shiftwidth的值,两者保持一致,方便统一缩进.
set softtabstop=-1

" 设置颜色主题,适用于黑色背景.
colorscheme slate

" 创建一个新的 MyTabSpace 组,并设置它的颜色
highlight MyTabSpace ctermfg=darkgrey

" 指定tab字符和空格的颜色组为MyTabSpace,不同字符串之间用|隔开,要使用\|转义.
match MyTabSpace /\t\| /

" 针对特定类型的代码文件,设置显示Tab键和行尾空格以便在查看代码时注意到它们
" TODO 后续查看代码如果体验不好再改成用map映射快捷键开关list来动态切换显示
autocmd FileType c,cpp,java,xml setlocal list | set listchars=tab:>~,trail:.

" 配置 gtags 插件,用于在函数之间跳转,方便查看源代码.
" 参考 gtags-cscopde.vim 的注释,添加下面语句来使用 ':tag' 和 '<C-]>'
set cscopetag
" 设置 cscopetag 后,由于gtags-cscopde默认没有启动,还需要进行下面的设置,
" 结合这两个设置, gtags 就可以使用Ctrl-]键来跳转到函数定义处.
let GtagsCscope_Auto_Load = 1
" 配置 GtagsCscope_Auto_Load = 1 后,在没有GTAGS文件的目录下使用vim,会提示
" Gtags-cscope: GTAGS not found.
" Press ENTER or type command to continue
" 需要按回车才会打开文件.如果要去掉这个报错,需要设置GtagsCscope_Quiet = 1
let g:GtagsCscope_Quiet = 1
" 设置只有一个匹配结果时,不显示quickfix窗口
let g:Gtags_Close_When_Single = 1

" 配置 quickfix 相关命令的快捷键. 可以用:map命令查看vim已有的快捷键映射.
nnoremap <F2> :cclose<CR>
nnoremap <F3> :cn<CR>
nnoremap <F4> :cp<CR>

" vim 用 map 命令来映射快捷键,它前面可以加一些前缀来对应不同的场景.
" 下面 map 前面的 nore 表示非递归. nore 前面的n表示只在普通模式下生效.
" 即,基于下面的配置,在插入模式下,按F6没有这个映射效果.插入模式对应i.
" 下面配置cscope查找文件命令的快捷键为F6,由于需要手动输入文件名,不要加<CR>
nnoremap <F6> :cs find f<Space>

" 如果要去掉高亮显示搜索到的内容,需要再次搜索一些不存在的字符串,比较麻烦.可以
" 在vim的命令行中执行nohlsearch命令去掉当前高亮.下面以:开头表示在命令行执行.
nnoremap <F9> :nohlsearch<CR>

" 插入模式下也用F9来去掉搜索高亮.下面的<C-o>表示CTRL-O,在插入模式执行一次命令
inoremap <F9> <C-o>:nohlsearch<CR>
```

### 5.4
总有一句话让你明白，总有有个方法适合你。我相信性空，也相信，这性，在地域，时间中逐渐填充成一种形式。当然也有基因的遗传。 所以最好的方式就是，走一步， 向后看几步，向前想几步。不断的在时间中继续用更好的方式进步。
从宇宙观，价值观，方法论，逻辑思维，看，听，说，想，表达。继续来和自己的基因，和已被填满的种种，重新整合。该抛的抛，该变通的变通，该坚持的坚持，该学习的学习，该引进的引进，该探索的探索。这过程本就是奇迹，美好，种种，答案不需外求。

explicitly \ ik-ˈspli-sət-lē 注意发音，k其实就应该是k，要不然直接标g好了
university \ ˌyü-nə-ˈvər-sə-tē s不变，说明非爆破音确实不属于规则

https://fenghe.us/software-router-lede-x64-installation/
[软路由firmware](http://firmware.koolshare.cn/LEDE_X64_fw867/)
https://m0n0.ch/wall/physdiskwrite.php
找到你的U盘盘符（我这里盘符是U，以我的为例），然后在命令行输入：

U:
physdiskwrite -u 镜像名
然后选择安装到哪个盘，选择非Windows系统盘的那个盘（一般来说是信息量多的那个，我这里是选择0号盘）。
关机后重新开启电源，然后用网线连接软路由和电脑。

把电脑的IP地址手动设置成192.168.1.2后保存。
接下来在浏览器地址栏输入192.168.1.1，输入密码koolshare


[punctuation](https://www.ef.edu/english-resources/english-grammar/punctuation/)
https://courses.lumenlearning.com/boundless-writing/
https://www.grammarbook.com/grammar/cnt_gram.asp
[english learning](https://prowritingaid.com/grammar/1000133/When-should-I-use-a-hyphen-between-two-words)
https://www.englishgrammar101.com/module-14/additional-punctuation/lesson-4/hyphens
https://owl.purdue.edu/owl/general_writing/punctuation/punctuation/index.html

### 5.3
https://www.appannie.com/en/apps/ios/top/united-kingdom/news/iphone/
https://www.newsbreak.com/
https://www.smartnews.com/
https://twitter.com/
https://reddit.com/
你才见过多少事，多少人啊。
我从春天走来，经过夏天的洗礼，秋天的无奈，到冬天的不舍。
再不会再重来，能再有机会学习，是幸福的，幸运的。

## social networking
facebook
message
discord
whatsapp
hangout
telegram
omegle
yolo

wechat
weibo
小红书
知乎
多闪

## news
今日头条
twitter
reddit
news break
smart news
quora

## books
audible audiobooks
amazon kindle
wattpad - read
dreame
yarn - chat

7猫小说
番茄小说
喜马拉雅FM
微信读书

学习英语与用英语来学习
学习为主而不是英语，学的有趣，触动人心
兴趣为主，难易其次 肯定有一条线，就像单词，总有一个例句，总有一篇文章，一个方式能让你走到终极。
生就是一瞬间的事，这一瞬，百万个可能

中国是大，国外是小，这样Pk，终归是要在大的基础上，不断细分，才能了解宇宙
一切都在消散，衰变，在最有时间的年华，从来不惧任何，才是最美的生命。

exploid 
n. \ ˈek-ˌsplȯit

v. \ ik-ˈsplȯit 
Children are being exploited in many of these factories.

词典例句
http://googledictionary.freecollocation.com/meaning?word=exploit
https://inspirassion.com/en/phrase/exploit

### 4.30
[开源世界旅行手册](http://treelib.com/book-detail-id-25-aid-1182.html)
[codebug](https://t.codebug.vip/list-6.htm)


urxvt解惑(https://qa.1r1g.com/sf/ask/993049991/)
https://github.com/appleshan/dotfiles/blob/stow/urxvt/.Xdefaults
https://www.muzilong.cn/storage/html/76/www.jianshu.com/p/9e8fe8892b61.html
https://www.bbsmax.com/A/A2dmR9yWze/
https://cnfczn.com/notes/linux/%E8%BD%BB%E9%87%8F%E7%BA%A7X%E4%B8%8B%E7%BB%88%E7%AB%AF%E6%A8%A1%E6%8B%9F%E5%99%A8-rxvt-unicode(urxvt)
http://yuex.in/post/2013/09/terminal-switching.html
https://cnfczn.com/notes/linux/%E8%BD%BB%E9%87%8F%E7%BA%A7X%E4%B8%8B%E7%BB%88%E7%AB%AF%E6%A8%A1%E6%8B%9F%E5%99%A8-rxvt-unicode(urxvt)
https://bbs.archlinuxcn.org/viewtopic.php?id=5712
https://sillydong.com/mysa/mylinux/urxvt.html
https://segmentfault.com/a/1190000020859490
https://wiki.archlinux.org/index.php/Rxvt-unicode
https://wiki.archlinux.org/index.php/X_resources
https://unix.stackexchange.com/questions/363276/xinitrc-not-loading-xresources
https://bbs.archlinux.org/viewtopic.php?id=71742
https://unix.stackexchange.com/questions/158787/load-x-resources-when-kde-starts-on-linux-mint
https://www.dwarmstrong.org/xresources/
修改完资源文件后，需运行以下命令使配置生效，或重启X会话。一般我们选择前者：

debian:~# xrdb .Xresources
xrdb ~/.Xresources
```
xrdb -merge ~/.Xresources
```

一些博客
http://www.huangpan.net/

### 4.29
[urvxt配置](https://addy-dclxvi.github.io/post/configuring-urxvt/)
termite
URxvt (rxvt-unicode)
Alacritty
yakuake
konsole
基本上这5个

role 总有一个句子让你习得一个单词
https://www.etymonline.com/word/role
https://www.yourdictionary.com/role
https://findwords.info/term/role
https://www.englishlearner.com/dictionary/role
https://www.wordnik.com/words/role

https://www.ibm.com/developerworks/cn/linux/l-vim-script-5/index.html

spacevim windows配置
```
[options]
    # set spacevim theme. by default colorscheme layer is not loaded,
    # if you want to use more colorscheme, please load the colorscheme
    # layer
    colorscheme = "gruvbox"
    colorscheme_bg = "dark"
    # Disable guicolors in basic mode, many terminal do not support 24bit
    # true colors
    enable_guicolors = true
    guifont = "MesloLGMDZ NF:h12"
    # Disable statusline separator, if you want to use other value, please
    # install nerd fonts
    statusline_separator = "arrow"
    statusline_inactive_separator = "bar"
    buffer_index_type = 4
    windows_index_type = 3
    enable_tabline_filetype_icon = true
    enable_statusline_mode = true
    statusline_unicode_symbols = false
    # Enable vim compatible mode, avoid changing origin vim key bindings
    vimcompatible = false
    bootstrap_before = "myspacevim#before"
    bootstrap_after  = "myspacevim#after"

# Enable autocomplete layer
[[layers]]
name = 'autocomplete'
auto-completion-return-key-behavior = "complete"
auto-completion-tab-key-behavior = "cycle"
auto_completion_enable_snippets_in_popup = false

[[layers]]
name = 'shell'
default_position = 'top'
default_height = 30

[[layers]]
  name = "denite"

[[layers]]
  name = "tools"
  
[[layers]]
  name = "VersionControl"

[[layers]]
  name = "git"
  
[[layers]]
  name = "lang#sh"

[[layers]]
  name = "lang#markdown"
```

spacevim.vim
```
function!  myspacevim#before() abort
  let g:spacevim_default_indent = 4
  let g:spacevim_max_column = 79
  au FileType markdown setlocal wrap
  au FileType  json setlocal shiftwidth=2 softtabstop=2
  au FileType html setlocal shiftwidth=2 softtabstop=2
# 注释不能放里面
#  au is short for autocmd，设置文件类型不能放一起
endfunction


function!  myspacevim#after() abort

endfunction
```

[cn下md慢慢看](https://github.com/SpaceVim/SpaceVim/tree/master/docs/cn)

https://github.com/SpaceVim/SpaceVim/blob/master/docs/conventions.md

https://gowa.club/Vim/ultisnips%E7%9A%84readme%E6%96%87%E6%A1%A3%E4%B8%AD%E6%96%87.html

https://www.webdictionary.co.uk/words/capitalization

单词搜索，这个绝了 https://onelook.com/?loc=olthes1&w=capitalization
```
**General**

 (36 matching dictionaries)

1. [apple](https://www.merriam-webster.com/dictionary/apple): Merriam-Webster.com [[home](https://www.merriam-webster.com/), [info](https://www.onelook.com/?d=mwd&qs=apple)] 
2. [apple](http://www.oxforddictionaries.com/us/definition/american_english/apple): Oxford Dictionaries [[home](http://www.oxforddictionaries.com/us), [info](https://www.onelook.com/?d=oxf&qs=apple)] 
3. [apple](https://www.ahdictionary.com/word/search.html?q=apple): American Heritage Dictionary of the English Language [[home](https://www.ahdictionary.com/), [info](https://www.onelook.com/?d=ahd&qs=apple)] 
4. [apple](http://www.collinsdictionary.com/dictionary/english/apple): Collins English Dictionary [[home](http://www.collinsdictionary.com), [info](https://www.onelook.com/?d=cln&qs=apple)] 
5. [apple](http://www.vocabulary.com/definition/apple): Vocabulary.com [[home](http://www.vocabulary.com), [info](https://www.onelook.com/?d=vcb&qs=apple)] 
6. [apple](http://www.macmillandictionary.com/dictionary/american/apple): Macmillan Dictionary [[home](http://www.macmillandictionary.com/), [info](https://www.onelook.com/?d=mac&qs=apple)] 
7. [Apple](http://www.wordnik.com/words/Appleâ), [Apple](http://www.wordnik.com/words/Apple), [apple](http://www.wordnik.com/words/apple): Wordnik [[home](http://www.wordnik.com/), [info](https://www.onelook.com/?d=rdn&qs=apple)] 
8. [apple](http://dictionary.cambridge.org/dictionary/british/apple): Cambridge Advanced Learner's Dictionary [[home](http://dictionary.cambridge.org/), [info](https://www.onelook.com/?d=cie&qs=apple)] 
9. [Apple](http://www.infovisual.info/01/033_en.html): InfoVisual Visual Dictionary [[home](http://www.infovisual.info/), [info](https://www.onelook.com/?d=ivz&qs=apple)] 
10. [Apple](http://en.wiktionary.org/wiki/Apple), [apple](http://en.wiktionary.org/wiki/apple): Wiktionary [[home](http://www.wikipedia.org), [info](https://www.onelook.com/?d=wkt&qs=apple)] 
11. [apple](http://www.yourdictionary.com/apple): Webster's New World College Dictionary, 4th Ed. [[home](http://www.yourdictionary.com/), [info](https://www.onelook.com/?d=yda&qs=apple)] 
12. [apple](http://www.wordsmyth.net/live/home.php?script=search&matchent=apple&matchtype=exact): The Wordsmyth English Dictionary-Thesaurus [[home](http://www.wordsmyth.net/), [info](https://www.onelook.com/?d=wed&qs=apple)] 
13. [apple](http://dictionary.infoplease.com/apple): Infoplease Dictionary [[home](http://www.infoplease.com/dictionary.html), [info](https://www.onelook.com/?d=ipd&qs=apple)] 
14. [Apple](http://dictionary.reference.com/search?q=Apple), [apple](http://dictionary.reference.com/search?q=apple): Dictionary.com [[home](http://www.dictionary.com/), [info](https://www.onelook.com/?d=ict&qs=apple)] 
15. [apple](http://www.etymonline.com/index.php?term=apple): Online Etymology Dictionary [[home](http://www.etymonline.com/), [info](https://www.onelook.com/?d=ety&qs=apple)] 
16. [Apple](http://www.ultralingua.net/index.html?service=ee&text=), [apple](http://www.ultralingua.net/index.html?service=ee&text=): UltraLingua English Dictionary [[home](http://www.ultralingua.net), [info](https://www.onelook.com/?d=ult&qs=apple)] 
17. [apple](http://dictionary.cambridge.org/results.asp?dict=A&searchword=apple): Cambridge Dictionary of American English [[home](http://dictionary.cambridge.org/), [info](https://www.onelook.com/?d=cim&qs=apple)] 
18. [apple](http://dictionary.cambridge.org/results.asp?searchword=apple&dict=I): Cambridge International Dictionary of Idioms [[home](http://dictionary.cambridge.org/), [info](https://www.onelook.com/?d=cii&qs=apple)] 
19. [APPLE](https://en.wikipedia.org/wiki/APPLE), [Apple (Fruit)](https://en.wikipedia.org/wiki/Apple (Fruit)), [Apple (album)](https://en.wikipedia.org/wiki/Apple (album)), [Apple (artwork)](https://en.wikipedia.org/wiki/Apple (artwork)), [Apple (automobile)](https://en.wikipedia.org/wiki/Apple (automobile)), [Apple (band)](https://en.wikipedia.org/wiki/Apple (band)), [Apple (company)](https://en.wikipedia.org/wiki/Apple (company)), [Apple (disambiguation)](https://en.wikipedia.org/wiki/Apple (disambiguation)), [Apple (fruit)](https://en.wikipedia.org/wiki/Apple (fruit)), [Apple (name)](https://en.wikipedia.org/wiki/Apple (name)), [Apple (symbolism)](https://en.wikipedia.org/wiki/Apple (symbolism)), [Apple (system on chip)](https://en.wikipedia.org/wiki/Apple (system on chip)), [Apple (technology company)](https://en.wikipedia.org/wiki/Apple (technology company)), [Apple](https://en.wikipedia.org/wiki/Apple), [The Apple (TOS episode)](https://en.wikipedia.org/wiki/The Apple (TOS episode)): Wikipedia, the Free Encyclopedia [[home](https://www.wikipedia.org), [info](https://www.onelook.com/?d=wik&qs=apple)] 
20. [Apple](http://www.onelook.com/?other=web1913&w=Apple): Online Plain Text English Dictionary [[home](http://www.mso.anu.edu.au/~ralph/OPTED/), [info](https://www.onelook.com/?d=anu&qs=apple)] 
21. [apple](http://www.webster-dictionary.org/definition/apple): Webster's Revised Unabridged, 1913 Edition [[home](http://www.webster-dictionary.org), [info](https://www.onelook.com/?d=art&qs=apple)] 
22. [apple](http://www.rhymezone.com/r/rhyme.cgi?Word=apple): Rhymezone [[home](http://www.rhymezone.com/), [info](https://www.onelook.com/?d=rhy&qs=apple)] 
23. [apple](http://www.allwords.com/query.php?SearchType=3&Keyword=apple&goquery=Find+it!&Language=ENG): AllWords.com Multi-Lingual Dictionary [[home](http://www.allwords.com/), [info](https://www.onelook.com/?d=all&qs=apple)] 
24. [apple](http://webstersdictionary1828.com/Dictionary/apple): Webster's 1828 Dictionary [[home](http://webstersdictionary1828.com/), [info](https://www.onelook.com/?d=smo&qs=apple)] 
25. [Apple](http://www.bibliomania.com/2/3/174/1111/15785/1.html#A613): E Cobham Brewer, The Reader's Handbook [[home](http://www.bibliomania.com/Reference/Readers/), [info](https://www.onelook.com/?d=bli&qs=apple)] 
26. [Apple](http://www.bartleby.com/81/823.html): Dictionary of Phrase and Fable (1898) [[home](http://www.bartleby.com/81/), [info](https://www.onelook.com/?d=dpf&qs=apple)] 
27. [Apple](http://encarta.msn.com/encnet/refpages/RefArticle.aspx?refid=761574393): Encarta® Online Encyclopedia, North American Edition [[home](http://encarta.msn.com/encnet/refpages/artcenter.aspx), [info](https://www.onelook.com/?d=eca&qs=apple)] 
28. [Apple](http://www.1911encyclopedia.org/Apple): 1911 edition of the Encyclopedia Britannica  [[home](http://1911encyclopedia.org/index.htm), [info](https://www.onelook.com/?d=enc&qs=apple)] 
29. [apple](http://www.freedictionary.org/?Query=apple): Free Dictionary [[home](http://www.freedictionary.org), [info](https://www.onelook.com/?d=fdn&qs=apple)] 
30. [apple](http://www.mnemonicdictionary.com/word/apple): Mnemonic Dictionary [[home](http://www.mnemonicdictionary.com/), [info](https://www.onelook.com/?d=mne&qs=apple)] 
31. [apple](http://poets.notredame.ac.jp/cgi-bin/wn?cmd=wn&word=apple): WordNet 1.7 Vocabulary Helper [[home](http://poets.notredame.ac.jp/cgi-bin/wn), [info](https://www.onelook.com/?d=ntr&qs=apple)] 
32. [Apple](http://lookwayup.com/lwu.exe/lwu/d?s=f&w=Apple), [apple](http://lookwayup.com/lwu.exe/lwu/d?s=f&w=apple): LookWAYup Translating Dictionary/Thesaurus [[home](http://lookwayup.com/free), [info](https://www.onelook.com/?d=ook&qs=apple)] 
33. [apple](http://www.thefreedictionary.com/apple): Dictionary/thesaurus [[home](http://www.thefreedictionary.com/), [info](https://www.onelook.com/?d=tfd&qs=apple)] 
34. [apple](http://www.onelook.com/pronounce/En-us-apple.WAV): Wikimedia Commons US English Pronunciations [[home](http://commons.wikimedia.org/wiki/Category:English_pronunciation), [info](https://www.onelook.com/?d=wms&qs=apple)] 





**Art**

 (5 matching dictionaries)

1. [apple](http://whatscookingamerica.net/Glossary/A.htm): Linda's Culinary Dictionary [[home](http://whatscookingamerica.net/Glossary/GlossaryIndex2.htm), [info](https://www.onelook.com/?d=ats&qs=apple)] 
2. [apple](http://www.epicurus.com/Glossary/spanish/glossary.php?&page=6&letter=a): Epicurus.com Spanish Glossary [[home](http://www.epicurus.com/Glossary/), [info](https://www.onelook.com/?d=cua&qs=apple)] 
3. The Apple: Jazz Humor [[home](http://www.allaboutjazz.com/speak.htm), [info](https://www.onelook.com/?d=lla&qs=apple)] 
4. [Apple](http://homepages.tscnet.com/omard1/a.htm#apple): Natural Magick  [[home](http://homepages.tscnet.com/omard1/jportat5.html), [info](https://www.onelook.com/?d=tsc&qs=apple)] 
5. [Apple](http://www.umich.edu/~umfandsf/symbolismproject/symbolism.html/A/apple.html): Dictionary of Symbolism [[home](http://www.umich.edu/~umfandsf/symbolismproject/symbolism.html/), [info](https://www.onelook.com/?d=umi&qs=apple)] 





**Business**

 (1 matching dictionary)

1. [APPLE](http://www.rma.usda.gov/help/cropabbr.html): Glossary of Crop Abbreviations [[home](http://www.rma.usda.gov/help/cropabbr.html), [info](https://www.onelook.com/?d=gca&qs=apple)] 





**Computing**

 (6 matching dictionaries)

1. [APPLE](http://foldoc.org//APPLE): Free On-line Dictionary of Computing [[home](http://foldoc.org/), [info](https://www.onelook.com/?d=fol&qs=apple)] 
2. [Apple](http://www.netlingo.com/dictionary/a.php): Netlingo [[home](http://www.netlingo.com/dictionary/a.php), [info](https://www.onelook.com/?d=net&qs=apple)] 
3. [Apple](http://www.csgnetwork.com/glossarya.html#Apple): Computer Telephony & Electronics Dictionary and Glossary [[home](http://www.csgnetwork.com/glossary.html), [info](https://www.onelook.com/?d=csg&qs=apple)] 
4. [Apple](http://www.techterms.com/definition/apple): Tech Terms Computer Dictionary [[home](http://www.techterms.com/), [info](https://www.onelook.com/?d=ech&qs=apple)] 
5. [Apple](http://www.learnthenet.com/french/glossary/apple.htm): Internet Terms [[home](http://www.learnthenet.com/english/index.html), [info](https://www.onelook.com/?d=leb&qs=apple)] 
6. [Apple (Computers)](http://encyclopedia2.thefreedictionary.com/Apple+(Computers)), [Apple (company)](http://encyclopedia2.thefreedictionary.com/Apple+(company)), [Apple (computer)](http://encyclopedia2.thefreedictionary.com/Apple+(computer)), [Apple (fruit)](http://encyclopedia2.thefreedictionary.com/Apple+(fruit)), [Apple (tree)](http://encyclopedia2.thefreedictionary.com/Apple+(tree)), [Apple ///](http://encyclopedia2.thefreedictionary.com/Apple+%2f%2f%2f), [apple](http://encyclopedia2.thefreedictionary.com/apple): Encyclopedia [[home](http://www.thefreedictionary.com/), [info](https://www.onelook.com/?d=tfe&qs=apple)] 





**Medicine**

 (2 matching dictionaries)

1. [APPLE](http://www.mondofacto.com/facts/dictionary?APPLE), [apple](http://www.mondofacto.com/facts/dictionary?apple): online medical dictionary [[home](http://www.mondofacto.com/dictionary/), [info](https://www.onelook.com/?d=dof&qs=apple)] 
2. [Apple (fruit)](http://medical-dictionary.thefreedictionary.com/Apple+(fruit)), [Apple (tree)](http://medical-dictionary.thefreedictionary.com/Apple+(tree)), [apple](http://medical-dictionary.thefreedictionary.com/apple): Medical dictionary [[home](http://www.thefreedictionary.com/), [info](https://www.onelook.com/?d=tff&qs=apple)] 





**Miscellaneous**

 (5 matching dictionaries)

1. APPLE: Navajo Code Talkers' Dictionary [[home](http://www.history.navy.mil/faqs/faq61-4.htm), [info](https://www.onelook.com/?d=ist&qs=apple)] 
2. [Apple](http://www.barnonedrinks.com/tips/dictionary/a/apple-128.html): Bar-Nones Dictionary of Drinking [[home](http://www.barnonedrinks.com/tips/dictionary/), [info](https://www.onelook.com/?d=arn&qs=apple)] 
3. [APPLE](http://www.acronymfinder.com/af-query.asp?Acronym=APPLE&String=exact&p=ol): Acronym Finder [[home](http://www.AcronymFinder.com/), [info](https://www.onelook.com/?d=mtn&qs=apple)] 
4. [APPLE](http://www.abbreviations.com/bs.asp?st=APPLE): AbbreviationZ [[home](http://www.abbreviations.com), [info](https://www.onelook.com/?d=tan&qs=apple)] 
5. [apple](http://idioms.thefreedictionary.com/apple): Idioms [[home](http://www.thefreedictionary.com/), [info](https://www.onelook.com/?d=tfj&qs=apple)] 





**Religion**

 (1 matching dictionary)

1. [Apple](http://www.ccel.org/ccel/easton/ebd2.html?term=Apple): Easton Bible [[home](http://www.ccel.org/ccel/easton/ebd2.EBD.html), [info](https://www.onelook.com/?d=eas&qs=apple)] 





**Science**

 (3 matching dictionaries)

1. [Apple](http://www.backyardgardener.com/plantname/pda_b01a.html): Botanical Name listing of Plants [[home](http://www.backyardgardener.com/plantname/index.html), [info](https://www.onelook.com/?d=ack&qs=apple)] 
2. [Apple (Bitter)](http://www.botanical.com/botanical/mgmh/a/apple046.html), [Apple](http://www.botanical.com/botanical/mgmh/a/apple044.html): A Modern Herbal, 1931, by Mrs. M. Grieve [[home](http://www.botanical.com/botanical/mgmh/comindx.html), [info](https://www.onelook.com/?d=bot&qs=apple)] 
3. [Apple](http://mathworld.wolfram.com/Apple.html): Eric Weisstein's World of Mathematics [[home](http://mathworld.wolfram.com/), [info](https://www.onelook.com/?d=ewm&qs=apple)] 





**Slang**

 (2 matching dictionaries)

1. [apple (core)](http://www.peevish.co.uk/slang/a.htm): English slang and colloquialisms used in the United Kingdom [[home](http://www.peevish.co.uk/slang/), [info](https://www.onelook.com/?d=pee&qs=apple)] 
2. [A.P.P.L.E](http://www.urbandictionary.com/define.php?term=A.P.P.L.E.), [apple](http://www.urbandictionary.com/define.php?term=apple ), [apple (core)](http://www.urbandictionary.com/define.php?term=apple (core)): Urban Dictionary [[home](http://www.urbandictionary.com), [info](https://www.onelook.com/?d=urb&qs=apple)] 





**Sports**

 (1 matching dictionary)

1. Apple: Croquet [[home](http://laplaza.org/~teddis/glossary.html), [info](https://www.onelook.com/?d=cro&qs=apple)] 
```

---------实修书籍---------
不少修行者，希望向我寻一个正法的‘入手处’。
最早的佛经道典，由于时代久远，以及文字与文化上的隔阂，很难让人读懂。
这里，推荐几本现代修行的正法书籍，跟这些书看下来，见地就会十分纯正，走不偏。
《当下的力量》埃克哈特·托尔
《与神对话1、2、3》尼尔·唐纳德·沃尔什
《山居性纪》吴光磊——性是种子，禅是花开（只看开头就误以为黄书，不多想想，中央编译出版社，会出黄书吗？：）
《深入浅出说心经》释戒悲——天涯论坛
巴夏视频系列——可在土豆网搜索关键字‘bashar’或是‘巴夏’，寻找你需要的短视频进行观看，可忽略外星人的部分，只看意识转化的部分。
《新世界——灵性的觉醒》埃克哈特·托尔
你结合上面推荐的资料，再去看下面的古典资料，一切都会变得简单易懂，无需任何翻译：
《心经》
《金刚经》
《清净经》
《道德经》
《马太福音》、《马可福音》、《路加福音》、《约翰福音》——不要去看《圣经》，这四本福音书就已经足够
《六祖坛经》
最后，给各位推荐一个读经的正确方法。
名为‘心读法’，需用感应而不是思辨。
没有古文功底，也不要去买那些翻译或是诠释的版本来看，这些版本的作者基本毫无见地，修行者看这些诠释，有害无益。
你只需一遍又一遍，反复的看原始版本便可。
看不懂就看不懂，看完了放一边，不要背诵。
隔一段时间，再重新拿起看一遍，每次你都会有截然不同的体会。
随着修行的进步，对生活体悟的增加，你每次看懂的东西也会更多一些。
唯有这样，你才能越过文字的表相，直接读取到文字背后的真实感悟。
这，才是正确的读经方法


### 4.28
## 今天感受到要了解掌握事物，要么从前往后看，演变，这个属于天才方式。另一种就是从后往前看，从具体应用去习得。这属于聪明人。其他方式都是不得法。
不断的寻找，思考，发现，总有一个句子是创造这个词的时候第一个句子
[Advanced Google Search Tips for Smarter Searching](https://www.coforge.com/blog/advanced-google-search-tips)

intext:foo
[english sentences](http://searchsentences.com/words/comprehensive-in-a-sentence)
[english sentences](http://www.englishcollocation.com/how-to-use/comprehensive)
https://www.translateen.com/sentence/comprehensive-in-sentence-examples/
https://www.wordhippo.com/what-is/sentences-with-the-word/comprehensive.html
https://sentencehouse.com/comprehensive/
[查单词](https://wordassociations.net/en/words-associated-with/Imply?button=Search)
[查单词](https://www.englishlearner.com/dictionary/imply)

- fairly 精辟的解释https://www.ldoceonline.com/dictionary/fairly
  - more than a little, but much less than very

- phonics \ ˈfä-niks 

- [英语惯用语块的习得研究](http://www.wenqujingdian.com/Public/editor/attached/file/20180612/20180612075925_79433.pdf)

自然拼读法phonics

- 隐喻
隐喻不仅是语言现象，而且是一种思维方式，是人类生存和认知的基本方式之一。它植根于语言、思维和文化中，对我们的行为活动和思维方式有着潜在的影响，这就形成了概念隐喻。
https://www.hotbak.net/key/%E8%AF%95%E8%AE%BA%E8%8B%B1%E8%AF%AD%E8%AF%8D%E6%B1%87%E4%B8%AD%E7%9A%84%E6%A6%82%E5%BF%B5%E9%9A%90%E5%96%BB%E6%80%8E%E6%A0%B7%E8%83%8C%E5%8D%95%E8%AF%8D.html

- thousands of young men came forward, willing to defend their country.

- [每次一个英语学习](https://language.chinadaily.com.cn/a/201912/11/WS5df0b2c9a310cf3e3557d82c.html)


post‧script /ˈpəʊsˌskrɪpt $ ˈpoʊs-/ noun [countable] (written abbreviation PS)

- imminent \ ˈi-mə-nənt 
  - Soon it became clear to everyone that war was imminent.

- about to
  - https://www.gymglish.com/en/gymglish/english-grammar/be-about-to
  - https://www.talkenglish.com/lessondetails.aspx?ALID=2018

- implication \ ˌim-plə-ˈkā-shən
  - a possible effect or result of an action or a dcision.
  - They failed to consider the wider implications of their actions.

- survey
  - a recent survey showed that 58 percent of people did not know where their heart is.


- surveyor
  - a person whose job is to measure and record the details of a reas of land.


- proposal
  - the committee put forward a proposal to reduce the time limit.


- imply //express or state indirectly.
  - to communicate an idea or feeling without saying it directly.
  - Are you implying (that) i'm fat?

- sense
  - an understanding about sth; an ability to judge sth.
  - He has a very good sense of direction.

- possess /pəˈzes/
  - to haev or own sth
  - He was charged with possessing a shotgun withoug a licence.
  - I'm afraid he doesn't possess a sense of humour.

- conscious
  - noticing or relizing sth. aware of wth
  - i was very conscious of the fact that I had to make a good impression.
  - aware
    - Knowing that sth exists, or having knowledge or experience of a particular thing.

- sense
  - https://www.englishlearner.com/dictionary/search.php?w=sense
    - make sense of something.
      - to understand wth, especially something difficult or complicated.
      - Can u make any sense of this article?

- apprehend \ ˌa-pri-ˈhend
  - to catch and arrest someone who has not obeyed the law
  - The police have finally apprehanded the killer.


- interpret \ in-ˈtər-prət
  -  to translate what someone is saying in one language into another language so that someone else can understand it

  - I speak Spanish. Would you like me to interpret for you?
  - to decide what the intended meaning of something is.
  - He interpreted her comments as an implicit criticism of the government.

- promise \ ˈprä-məs
  - We promised we wouldn't be late.

- intend
  - We intend to go to Australia next year.



### 4.27
- lower 非常好的解释 https://www.computerhope.com/jargon/l/lowercas.htm
	- Sometimes abbreviated as LC, lowercase is a typeface of small characters. For example, a, b, and c is lowercase and A, B, and C is uppercase. As long as the Shift key is not being pressed and the Caps lock is not active everything typed is in lowercase.

- sequence \ ˈsē-kwən(t)s  符合发音规则kw快速浊化合并

- escape character
	- https://www.computerhope.com/jargon/e/esc.htm
	-  Escape is shorthand for an escape character. An escape character is a single backward slash ( \ ) in Linux, programming, and regular expressions that treats the character after it as text and not a function. It can also be used to perform a special function. Below are some examples of how an escape could be used.
对单词的理解，要建立在实用的基础上

- interpretation
	- It is difficult for many people to accept a literal interpretation of the Bible.

========================
vim 在command 模式下粘贴
https://vim.fandom.com/wiki/Copy,_cut_and_paste

http://vimregex.com/ %作用
http://vimdoc.sourceforge.net/htmldoc/pattern.html
https://www.runoob.com/regexp/regexp-syntax.html
https://yianwillis.github.io/vimcdoc/doc/pattern.html#pattern.txt


g/\%(^\1\n\)\@<=\(.*\)$/d
g/                     /d  <-- Delete the lines matching the regexp
            \@<=           <-- If the bit following matches, make sure the bit preceding this symbol directly precedes the match
                \(.*\)$    <-- Match the line into subst register 1
  \%(     \)               <-- Group without placing in a subst register.
     ^\1\n                 <-- Match subst register 1 followed the new line between the 2 lines

g/^\(.*\)\n\1$/d
g/\%(^\1\n\)\@<=\(.*\)$/d
g/\v%(^\1\n)@<=(.*)$/d

. 任意字符 
* 0或者任意次
\n新的一行
\1 括号内相同的内容
$末尾 代表结尾以前和之前一样
/d删除

% the whole file. The same as 1,$

==============

regex
https://www.computerhope.com/unix/regex-quickref.htm
https://www.petefreitag.com/cheatsheets/regex/
https://www.rexegg.com/regex-quickstart.html#chars
https://vim.fandom.com/wiki/Uniq_-_Removing_duplicate_lines
http://vimregex.com/


### 4.25
[awesome-cheatsheets](https://github.com/LeCoupa/awesome-cheatsheets/blob/master/tools/vim.txt)
### CURSOR MOVEMENTS
- w //字符，符号"@$", "#%^&*()", :"等算成不同的几类,跳过空格
- W //所有字符符号算一类，空格跳过
- ge //jump backward to end of words

- ^ //first non-black character of line

- +// enter// move line downwards, non blank character

- -// move line upwards

- ng// :n// go to line n

- ]] //开头是{会调到，其他掠过直接到最后一行

- fx // search line forward for "x"
- Fx // search line backward for "x"

- tx // search line forward before "x"
- Tx // search line backward before "x"

### [mark](https://github.com/SpaceVim/SpaceVim/blob/master/docs/documentation.md)
- [源码](https://github.com/SpaceVim/SpaceVim/blob/master/autoload/SpaceVim/layers/tools.vim)


### 4.24
https://epdf.pub/
http://www.pdfdownload.online/
https://www.scribd.com/
https://www.pdfdrive.com/
https://www.engbookspdf.com/books-drive/English-Made-Easy-Volume2-New-ESL-Approach
http://dl.booktolearn.com/ebooks2/foreignlanguages/english/9780804837361_english_made_easy_volume_one_40ef.pdf
https://freekidsbooks.org/
https://www.8freebooks.net/books/children/
http://pdfcorner.com/


找书
https://www.barnesandnoble.com/b/kids-books/_/N-8qc
https://www.booktrust.org.uk/booklists/1/
https://bilingualkidspot.com/
http://www.magickeys.com/books/
https://deseretbook.com/t/books/childrens
https://bookroo.com/books

在线阅读
https://www.churchofjesuschrist.org/study/scriptures?lang=eng
比如:https://www.churchofjesuschrist.org/study/history/saints-v2/part-1/01-gather-up-a-company?lang=eng
http://www.espressoenglish.net/wp-content/uploads/2012/07/Free-Grammar-Ebook-Level-2.pdf

- sacred \ ˈsā-krəd 注意发音gre无d
- His daily routine is absolutely sacred to him.

- routine
- there's no set/fixed routine at work - every day is different

###４.23

[tmux教程](https://louiszhai.github.io/2017/09/30/tmux/#%E5%9F%BA%E6%9C%AC%E6%A6%82%E5%BF%B5)

http://vimdoc.sourceforge.net/htmldoc/motion.html#motion.txt
https://vim.fandom.com/wiki/All_the_right_moves
https://docs.oracle.com/cd/E19253-01/806-7612/6jgfmsvqf/index.html
https://vimhelp.org/motion.txt.html

- del:

> :foo,food //删除foo到foo包含的所有行

>  :foo,$d //删除从foo到末尾的所有

- delete one character
> x // 4x

- delete one character before the cursor
> X

- deleting a word or part of a word
> dw // 将cursor移到单词开头，或许要保留的部分后面，从光标处删除到空格

- deleting a line
> dd

- choose:

  go to line:fooG

  Press "V"

  typing: fooG

- 选中所在行到foo绝对行号并包括在内的所有行

  ctrl-g //where you are in the file<!--  显示在文件中位置 -->

- lowercase and uppercase

  - gu // lowercase
  - gU // uppercase
  
- bring line foo to top of your screen
- zt

- bing to middle of screen
- z.

- bring to bottom of screen
- zb

- 如果需要让光标在上中下
> H M L

- page forward one screen
> ctrl f

- page backward one screen
> ctrl b

- one-half screen
> ctrl u

> ctrl d

## move the cursor

- e // move to end of word
- W // move to beginning of next word after a whitespace"无视任何符号"
- B // 与上面相反
- E // move to end of word before a whitespace"单词末尾，遇到空格才算完整单词"

## change

- cw // change a word, 需要先移到单词开头
- cW// 无视空格外所有连接符
- cc // change a line

- r // 替换cursor下的character

##　yank and paste

### 行的复制粘贴
- yy, Y // yank
- p // put below粘贴在光标所在下行
- P // put above


### english

- mnemonic
  - a sentence or short poem that you use for helping you to remember something.
    - rhyme
      - have the same lst sound
      - can u thing of a word that rhymes with "orange"?

- equivalent  \ i-ˈkwiv-lənt
  - a thing, amount, word, etc. that is equal in value, meaning or purpose to something else
  - Is there a French word that is the exact equivalent of the English word ‘home’?

### 4.22
先重要后次要，先总结后具体，先框架后细节，先结论后原因，先结果后过程，先论点后论据。
比较，抽象，概括
思维方法学，管理学
看待问题还需要全面去看待， 分析问题要尽可能做到全面了解对象、联系和中介等方面
http://m.xielwb.com/luojixuelunwen/92373_2.html
很重要的内容http://m.xielwb.com/luojixuelunwen/98731.html


https://www.kingr.top/2018/08/17/SpaceVim%E8%87%AA%E5%8A%A8%E6%8A%98%E8%A1%8C%E4%B8%8E%E8%87%AA%E5%8A%A8%E6%8D%A2%E8%A1%8C/
https://github.com/SpaceVim/SpaceVim/issues/1796

[缩进的值官方建议在bootstrap里面](https://github.com/SpaceVim/SpaceVim/blob/master/autoload/SpaceVim.vim)
https://vimhelp.org/motion.txt.html
https://vim.fandom.com/wiki/Category:Moving
https://github.com/SpaceVim/SpaceVim/blob/42ea773008cfde44e70504da1ab41da33691967f/doc/SpaceVim.txt

[修改参考init](https://github.com/SpaceVim/SpaceVim/blob/master/doc/SpaceVim.txt)
[源码配置](https://github.com/SpaceVim/SpaceVim/blob/master/autoload/SpaceVim.vim)
[前缀](https://github.com/SpaceVim/SpaceVim/blob/master/docs/cn/documentation.md)
### copy cut and paste in vim
    yy - Yank (copy) the current line, including the newline character.
    3yy - Yank (copy) three lines, starting from the line where the cursor is positioned.
    y$ - Yank (copy) everything from the cursor to the end of the line.
    y^ - Yank (copy) everything from the cursor to the start of the line.
    yw - Yank (copy) to the start of the next word.
    yiw – Yank (copy) the current word.
    y% - Yank (copy) to the matching character. By default supported pairs are (), {}, and []. Useful to copy text between matching brackets.


### 4.21
https://github.com/SpaceVim/SpaceVim/blob/master/autoload/SpaceVim/layers/edit.vim

插件列表
https://blog.csdn.net/cnsword/article/details/52797203

[terryma/vim-expand-region](https://github.com/terryma/vim-expand-region)
[参考](https://github.com/terryma/vim-expand-region/blob/master/doc/expand_region.txt)
around标示边缘被包括

visual selection模式 括号包括内才能选中括号,对全角符号不支持
ib () 内 parentheses 取不到文字外侧括号，哪怕如果在()上，也取不到
iB {} 内 braces
i] [] 内 bracket
il 1行iniside line 和大V模式一样效果
ie 整个文件
ab () 能取到文字外侧括号
ii 在 inside indent,遇到空行也失效,不包括缩进外侧空行。
ai 所有around indent，所有以此缩进为准的，包含空行，全部选中,遇到超出则失效


## 4.20
重点快捷
https://github.com/SpaceVim/SpaceVim/tree/master/autoload/SpaceVim/mapping

- 计算机单词查询 https://www.computerhope.com/jargon/t/tiling.htm
- likely
  - it's quite likely that we'll be in China this time next year.

- tendency \ ˈten-dən(t)-sē 
  - I have a tendency to talk too much when I'm nervous.

- inclination \ ˌin-klə-ˈnā-shən
  - You must follow your own inclinations when choosing a career.

- leaning
  - His parents could not comprehend his artistic leanings.

- recline \ ri-ˈklīn
  - She was reclining on a sofa.


- pending
  - The offer to buy is still pending. 


- accused \ ə-ˈkyüzd
  - to accuse somebody of murder


- trial
  - He is facing trial on numerous terrorism charges.


- in court of law

- bail
  - He was released/remanded on bail (of $100,000).

- bidirectional  \ ˌbī-də-ˈrek-shnəl
  - moving, functioning, or receiving signals in or from two, usually opposite, directions
  - Functioning in two directions.
    - function
    - to work in the correct way
    - we now have a functioning shower

- hormoun \ ˈhȯr-ˌmōn

- tissue \ ˈti-(ˌ)shü
  - a collection of cells that form the different parts of humans, animals and plants
  - muscle/brain/lung tissue

  - soft paper that is used for cleaning, especially your nose, and is thrown away after use, or a small rectangular piece of this:
  - a piece of soft paper, used especially as a handkerchief
    - handkerchief \ ˈhaŋ-kər-chəf  注意发音k,不变，同n l 规则
    - a small piece of material or paper that you use for blowing your nose, etc.
      - blow
      - blow your nose to clear your nose by blowing strongly through it into a tissue or handkerchief.


- downword adj.
  - moving or pointing towards a lower level






## 4.18

[spacevim en_doc](https://github.com/SpaceVim/SpaceVim/blob/master/docs/documentation.md)
[快捷键的具体出处](https://github.com/SpaceVim/SpaceVim/blob/master/autoload/SpaceVim/mapping/g.vim)
https://blog.csdn.net/netdxy/article/details/50553543



dd
什么是删除当前行
删除光标前后若干词

快速移动到某行，某精确位置
插入模式下粘贴
其他模式下粘贴
粘贴到具体位置

移动光标
复制 选中
复制行
剪切行
复制光标位置到行尾
删除至行尾
删除光标所在字符
替换
查找文件
搜索文本
跳转
buffer切换使用
搜索后:nohl清除高亮
- SPC s c 或者运行 命令 :nohlsearch 来取消搜索结果的高亮表示。
i模式下: ctrl-r % 当前文件名输入到文件

以下3种方式:
minibufferexplor
后期tmux
Nerdtree插件来实现多标签编辑。

快捷键设计

如果要保证buffer的切换像tab一样方便，肯定是要设置快捷键的，要不然总输入命令太慢了。

"按Ctrl+h 向左移动一个buffer
nnoremap <C-h> :bp<CR>
"按Ctrl+l 向右移动一个buffer
nnoremap <C-l> :bn<CR>
"按Ctrl+^ 关闭当前buffer
nnoremap <C-^> :bd<CR>


- buffers
- ls, buffers 列出载入到内存的缓冲列表
- SPC <Tab> 	切换至前一缓冲区，常用于两个缓冲区来回切换
- SPC b p , [ b 切换至前一个缓冲区，排除特殊插件的缓冲区
- SPC b n 	, ] b 切换至下一个缓冲区，排除特殊插件的缓冲区
- SPC b Y 	将整个缓冲区复制到系统剪切板
- SPC b P 	使用系统剪切板内容替换当前缓冲区
- SPC b e 	清除当前缓冲区内容，需要手动确认
- SPC b C-d 	删除其它所有缓冲区

在多窗口间跳转和改变窗口大小


[参考](https://wizardforcel.gitbooks.io/use-vim-as-ide/content/5.html)
- 折叠
有时为了去除干扰，集中精力在某部分代码片段上，我会把不关注部分代码折叠起来。vim 自身支持多种折叠：手动建立折叠（manual）、基于缩进进行折叠（indent）、基于语法进行折叠（syntax）、未更改文本构成折叠（diff）等等，其中，indent、syntax 比较适合编程，按需选用。增加如下配置信息：

注释 NERD Commenter

模版补全ultisnips

智能补全有两类实现方式：基于标签的(了解即可，限制多，麻烦)、基于语义的

2.屏幕翻页
Ctrl+u: 向上翻半屏
Ctrl+f: 向上翻一屏
Ctrl+d: 向下翻半屏
Ctrl＋b: 向下翻一屏

3.移动光标指令
移动光标普遍使用的是方向键，考虑兼容问题，vi定义太多的方向指令，下面只是一小小部分（常用的几个）：
space: 光标右移一个字符
Backspace: 光标左移一个字符
Enter: 光标下移一行
nG: 光标移至第n行首
n+: 光标下移n行
n-: 光标上移n行
n:光标移至第n行尾0:光标移至当前行首

: 光标移至当前行尾

快速跳转插件Easymotion

4.插入删除指令
常用插入、删除指令如下：
i：在当前光标前插入，光标后文本向后移
a：从当前光标后插入，光标后文本后移
I：在光标所在行首插入（第一个非空白字符前）
A：从光标所在行末插入
o: 在光标所在行下面新增一行（并进入输入模式）
O: 在光标所在行上方新增一行（并进入输入模式）
x: 删除光标所在字符，等同于[Delete]功能键
X: 删除光标前字符，相当与[Backspace]
dd: 删除光标所在的行
r: 修改光标所在字符
R: 替换当前字符及其后的字符，直到按 [ESC]
s: 从当前光标位置处开始，以输入的文本替代指定数目的字符
S: 删除指定数目的行，并以所输入文本代替之
do: 删至行首
d$: 删至行尾 
————————————————
版权声明：本文为CSDN博主「极客Geek」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/netdxy/article/details/50553543

https://yianwillis.github.io/vimcdoc/doc/help.html

https://github.com/SpaceVim/SpaceVim/blob/master/docs/layers/fzf.md 查看各个layer.md说明
 denite py3 SPC b b / liat all buffers


### 4.17
源码快捷键
https://github.com/SpaceVim/SpaceVim/blob/master/autoload/SpaceVim/default.vim

ctrl+end进入最下面

- 文件树目录新建文件 F3/SPC f t
> N 	在光标位置新建文件 
- 显示隐藏文件 .
- ctrl-r 刷新文件树

- 新建新标签 s t
> [Window] t 	新建新的标签页 
> SPC w F 	新建一个新的标签页 

- [ t 跳至前一个标签页
- ] t 跳至后一个标签页
- s w o 按顺序切换
- g r 跳至前一个标签

- [ w 跳至前一个窗口
- ] w 跳至后一个窗口
- 删除标签页 
- s t t 标签管理 x 删除 o 展开 r 重命名 n 新建 enter进入

- 删除标签 s t t 打开后 x 删除
- 删除文件及buffer s f D
- 删除窗口，如果就一个标签一个窗口，同删除标签 s w d
- 删除选中的窗口 s w D

- 最大化窗口 s w m
- 切换窗口 s w r
- q 关闭当前窗口 和s Q 效果一样,无视有文件
- s o 关闭其他窗口
- 新建buffer就是新建窗口s b N h左侧 l右侧 j下方 k 上方
- 窗口导航 u撤销按键 n向下翻页 p向上翻译
- tab 窗口切换 ctrl+上下左右箭头切换

- 保存文件:w, ctrl-s, SPC f s, SPC f S(保存所有),SPC f W(使用管理员保存)
- 定位到文件树中的文件位置 SPC f o
- 打开文件历史 SPC f r
- 复制并显示当前文件的绝对路径
[文件操作相关快捷键](https://github.com/SpaceVim/SpaceVim/blob/master/docs/cn/documentation.md#特殊-buffer)

待处理
移动
半屏
粘贴


### 4.16 
phton go raku js
vscode
https://viatsko.github.io/awesome-vscode/

key: Genealogical tree of programming languages
https://erkin.party/blog/190208/spaghetti/genealogy.png
python raku go

一下搜索名词借鉴的网站 ，可以查词组更好的了解一个词
- pivot
	- https://searchsentences.com/words/pivot-in-a-sentence
	- https://www.wordreference.com/definition/pivot
	- https://www.urbandictionary.com/define.php?term=Pivot

- graph 
	- https://www.ldoceonline.com/dictionary/graph
	- https://www.yourdictionary.com/graph
	- https://www.macmillandictionary.com/us/dictionary/american/graph_1 
	- https://dictionary.cambridge.org/us/dictionary/english/graph
	- https://www.thefreedictionary.com/graph
	- https://www.collinsdictionary.com/us/dictionary/english/graph
	- https://www.thesaurus.net/graph
	- https://kids.britannica.com/kids/article/graph/399910

- graph 
	- deinfition graph

- imaginary	- \ i-ˈma-jə-ˌner-ē
	- existing only in your mind or imagination

- axis 
 - in mathematics, one of the two fixed lines used for showing measurements or finding the position of points on a graph
 - the vertical/horizontal axis



## spacevim 探索
https://spacevim.org/development/#conventions
https://spacevim.org/conventions/
http://vimdoc.sourceforge.net/htmldoc/usr_41.html

alanding对话
:verbose imap <c-e>
imap
nmap
verbose nmap
入口是init.vim
help functions有函数可以查映射的啥
help list-functions

找个python库，看
python跟vim像
看不懂的就help搜
函数说明，关键字说明
https://realpython.com/python-requests/#getting-started-with-requests


### 4.15
词典
http://www.freedictionary.org/
https://www.daridictionary.org/
http://www.finedictionary.com
https://mnemonicdictionary.com/

auto pairs 自动补全成对符号
https://tc500.github.io/%E5%B7%A5%E5%85%B7%E9%93%BE/2019/02/08/%E9%AB%98%E6%95%88%E7%9A%84vim/#%E6%88%90%E5%AF%B9%E7%AC%A6%E5%8F%B7


https://blog.csdn.net/liuchenxia8/article/details/79652847
插件集合

auto-pairs.vim: 括号自动匹配
a.vim: 切换.h/.c文件
DoxygenToolkit.vim: 生成文档风格的注释
mark.vim: 高亮关键字
NERD_tree.vim: 文件列表
tagbar.vim: 函数列表
ctrlp.vim: 快速查找文件
gruvbox: 一个漂亮的主题
python-mode: 一组Python开发的工具集合
vim-airline: 漂亮的标签页和状态栏
vim-colorschemes: 一个主题集合包
vim-cpp-enhanced-highlight: 更精细的c/c++语法高亮
vim-surround: 快速给一段代码外面包裹括号/引号
Vundle.vim: vim的一个插件管理器
AutoComlPop + OmniCppComplete + SuperTab + ctags: 代码补全
ctags: 代码跳转(这货不是vim插件, 是一个linux工具)
syntastic: 语法检查
snipMate + vim-snippets: 代码片段

Spacevim:
jk == esc
[自动补全插件](https://github.com/SpaceVim/SpaceVim/blob/483b3285baf453495b8ba37b2bffdb4b99e8f0c9/docs/cn/layers/autocomplete.md)
shift + enter 解决补全buffer问题

https://github.com/SpaceVim/SpaceVim/tree/master/docs/cn


### 4.14
- stiff
	- The windows were stiff and she couldn't get them open.

spacevim 安装 prettier
https://spacevim.org/layers/lang/markdown/

1. windows 安装yarn 一定要先安装nodejs
- choco install nodejs
2. 安装yarn 
- choco install yarn
https://classic.yarnpkg.com/en/docs/install#windows-stable

## GUI Git Clients for windows

smartgit 

bitbucket :
sourcetree

gitlab :
sourcetree


github:GitHub Desktop 

https://helpx.adobe.com/photoshop/using/default-keyboard-shortcuts.html

Switch to Hand tool (when not in text-edit mode)
	

Temporarily activate Hand tool

Spacebar

https://helpx.adobe.com/cn/photoshop-elements/using/keys-selecting-moving-objects.html

spacevim插件路径
 cd .\Users\Administrator\.cache\vimfiles\repos\github.com\Shougo\vimproc.vim\ 
cygwin
镜像 
https://mirrors.tuna.tsinghua.edu.cn/cygwin/

binutils

gcc-core 
gcc-g++

mingw64-x86_64-gcc-core
mingw64-x86_64-gcc--fortran
mingw64-x86_64-gcc-g++

gdb

添加bin到环境

cygcheck -c cygwin
  然后依次输入gcc –version，g++ --version，make –version，gdb –version进行测试，如果都打印出版本信息和一些描述信息，非常高兴的告诉你，你的cygwin安装完成了！

- coordinate
-   coordinate something with something We try to coordinate our activities with those of other groups.
### 4.11

  

## PS

- [WEB设计指南！PS礼仪白皮书](http://hao.uisdc.com/ps/)

- [英文版](https://photoshopetiquette.com/)

  

- [快捷键图片](https://www.uisdc.com/photoshop-shortcuts)

- [快捷键](https://www.uisdc.com/photoshop-keyboard-shortcuts-guideline)

- [ip138](https://www.ip138.com/photoshop/)

- [adobe默认快捷键](https://helpx.adobe.com/cn/photoshop/using/default-keyboard-shortcuts.html)

  

- [45个设计师需要熟记的PS快捷键](https://www.uisdc.com/45-handy-photoshop-shortcuts)

  

## VIM

- [必知必会的 Vim 编辑器基础命令 ](https://linux.cn/article-12053-1.html?utm_source=index&utm_medium=more)

- [10 Methods to View Different File Formats in Linux](https://www.2daygeek.com/unix-linux-command-to-view-file/)

  

- route \ ˈrüt

  

- urban \ ˈər-bən

  

- promise \ ˈprä-məs

  

- emphasize \ ˈem(p)-fə-ˌsīz

Zoom tool

Hold down the Option/Alt key to access the zoom and use the scroll wheel to zoom in and out.
http://www.photoshopforphotographers.com/3101-1901/Help_guide/tp/Zoom_tool.html

Alt+scroll wheel >> zoom in/out
- photograph 
- a picture of something that you make with a camera. In spoken language people usually say photo

- zoom in
-  to show the object that is being photographed from closer/further away, with the use of a zoom lens

- lens
- a curved piece of glass or plastic that makes things look larger, smaller or clearer when you look through it


- approach

- a way of dealing with somebody/something; a way of doing or thinking about something such as a problem or a task

- We need to adopt a new approach to the problem.

  

- movement nearer to somebody/something in distance or time

- She hadn't heard his approach and jumped as the door opened.
- layout

- the way in which the different parts of something are arranged

- The user gradually becomes familiar with the layout of the keyboard.

### 4.10
[Windows 10下使用Neovim + SpaceVim](https://blog.csdn.net/How_key/article/details/88413220)

  

注：Git环境的默认路径是通过HOME环境变量还指定的，默认指定为%HOMEDRIVE%%HOMEPATH% 或 %USERPROFILE%

[Git](https://git-scm.com/download/win) 默认自动添加cmd文件夹变量

[Neovim](https://github.com/neovim/neovim/releases) 添加到环境变量

[SpaceVim](https://github.com/SpaceVim/SpaceVim)

1. git clone 错误: fatal: unable to access 'https://github.com/SpaceVim/SpaceVim.git/': Failed to connect to 127.0.0.1 port 1080: Connection refused

  

原由，我在$HOME 设置了代理

```

[user]

name = lan542662

email = kktt914968841@gmail.com

[https]

proxy = socks5h://127.0.0.1:1080

```

  

查询是否使用代理：git config --global http.proxy 可能是:socks5h://127.0.0.1:1080

取消代理：git config --global --unset http.proxy

  

https://gist.github.com/laispace/666dd7b27e9116faece6

  

git使用代理服务器

http://blog.useasp.net/archive/2015/08/26/config-git-proxy-settings-on-windows.aspx

```

Git支持四种协议 1 ，而除本地传输外，还有：git://, ssh://, 基于HTTP协议，这些协议又被分为哑协议（HTTP协议）和智能传输协议。对于这些协议，要使用代理的设置也有些差异：

  

使用 git协议 时，设置代理需要配置 core.gitproxy

使用 HTTP协议 时，设置代理需要配置 http.proxy

而是用 ssh协议 时，代理需要配置ssh的 ProxyCommand 参数

  

由于个人需求仅仅是HTTP的代理（相对来说，HTTP有比较好的通适性，Windows配置git/ssh比较棘手），设置的时候，只需要针对单个设置 http.proxy 即可，在需要使用代理的项目下面使用 git bash 如下命令进行设置 ——你的Uri和port可能和我的不同，你懂的。：

  

git config http.proxy http://127.0.0.1:8088 # 也可以是uri:port形式

  

这个是不需要鉴权的代理设置，如果需要鉴权，可能需要添加用户名密码信息：

  

git config http.proxy http://username:password@127.0.0.1:8088

  

如果git的所有项目都需要启用代理，那么可以直接启用全局设置：

  

git config --global http.proxy http://127.0.0.1:8088

  

为了确认是否已经设置成功，可以使用 --get 来获取：

  

git config --get --global http.proxy

  

这样可以看到你设置在global的 http.proxy 值。

  

需要修改的时候，再次按照上面的方法设置即可，git默认会覆盖原有的配置值。

  

当我们的网络出现变更时，可能需要删除掉原有的代理配置，此时需要使用 --unset 来进行配置：

  

git config --global --unset http.proxy

  

在命令之后，指定位置的设置值将会被清空，你可以再次使用 --get 来查看具体的设置情况。

  

如果使用了HTTPS，肯呢个会碰到HTTPS 证书错误的情况，比如提示： SSL certificate problem 。。。，此时，可以尝试将 sslVerify 设置为 false ：

  

git config --global http.sslVerify false

```

  
  
  

## Cmder 安装 Chocolatey

可用的软件包 https://chocolatey.org/packages

  
  

[windows系统变量](https://my.oschina.net/lixin891230/blog/534106)

echo %HOMEPATH% 看到是 C:\Users\Administrator 此处Administrator为当前登录用户名

  
  
  

%HOMEDRIVE% = C:\ --当前启动的系统的所在分区

  

%SystemRoot% = C:\WINDOWS --当前启动的系统的所在目录

  

%windir% = %SystemRoot% = C:\WINDOWS --当前启动的系统的所在目录

  

%USERPROFILE% = C:\Documents and Settings\(user) --user指你的用户名

  

%HOMEPATH% = \Documents and Settings\(user) --user指你的用户名

  

比如：桌面路径: echo %systemdrive%%homepath%\桌面

### 4.9

https://www.ostechnix.com/list-useful-bash-keyboard-shortcuts/

多行添加
https://my.oschina.net/u/1459307/blog/1859598/print
多行同列直接编辑
https://www.jianshu.com/p/50d5b6cfd73b

技巧https://blog.csdn.net/GSH_Hello_World/article/details/71479932

% 指匹配整个文件，s 是置换的意思，$ 代表匹配行尾的内容，最后的 g 则表示每行中匹配到的内容都要置换。

- [fox](https://portapps.io/app/phyrox-portable/)
- [waterfox browser](https://www.waterfox.net/download/)
- [firefox portable](https://www.firefox-usb.com/)

### palemoon key KKTTch..7
k-76ymt-g73td-8wgbv-svwjk-sjfga

- She lived with her partner

- sense
	- He has as very good sense of directinon.
	- There's no sense in (= it is not sensible) worrying about it now.

- sexual \ ˈsek-sh(ə-)wəl  k阻碍到省略

write down/ record

thesaurus \ thi-ˈsȯr-əs

idioms

synonym \ ˈsi-nə-ˌnim 

acronyms  \ ˈa-krə-ˌnim

统一短语词典 https://synonym.wordhippo.com/
https://synonym.tech/write_down
https://thesaurus.plus/synonyms/write_down
https://www.powerthesaurus.org
https://sinonimos-online.com/english/
https://reversedictionary.org/
https://www.wordreference.com/synonyms/


∞ 17 世纪 英国数学家沃利斯(John Wallis
神学、医学、天文、数学
[中国哲学](http://www.guoxue.com/lwtj/content/zhoujianming_zgzxtjjhl.htm)
http://www.sun0moon.com/me/index00.htm


- flow rate
	```
	- flow
	- the steady and continuous movement of something/somebody in one direction
	- to control the direction of flow

	- the continuous production or supply of something	
	- We are looking to improve data flow by up to 50%.
	- positive
	- good or useful
	- His family have been a very positive influence on him.

	- rate
	- a measurement of the speed at which something happens
	- At the rate you work, you'll never finish!

	- a measurement of the number of times something happens or something does something during a particular period
	- We have seen a reduction in the crime rate over the last 12 months.

	- reduction
	-  an act of making something less or smaller; the state of being made less or smaller
	
	- ampere / amp \ ˈam-ˌpir
	-  the unit for measuring electric current

	- magnitude
	- the great size or importance of something; the degree to which something is large or important
	- We did not realize the magnitude of the problem.
	- (uncountable) great size, importance, or effect
	- We hadn’t grasped the magnitude of the task we were facing.


	- grasp
	- to understand something completely
	-  They failed to grasp the importance of his words.
	```

### 4.8
类似github某个主题的索引

https://awesomeopensource.com/projects/vim-colorscheme

  

https://www.definitions.net/definition/pattern

  

- general

- my general impression of the place was good.

- In general, men are taller than women.

- So , apart from the bad ankle, how are you in general?

  

- format \ ˈfȯr-ˌmat 注意重音

- a pattern, plan, or arrangement:

- The meeting will have the usual format - introductory session, group work and then a time for reporting back.

  

- bring out

- to produce a new product and start to sell it

- The next year they brought out a low-priced car to compete with Ford.

  

- regular \ ˈre-gyə-lər

- She writes a regular column for a national newspaper.

- He was a regular visitor to her house.

- The key to good anti-virus software is regular updates.

- We also hold a regular monthly meeting.

  

- column \ ˈkä-ləm

- a regular newspaper or magazine article on a particular subject or by a particular journalist

- He writes a weekly column for the Daily News.

- a part of a newspaper, magazine or website that appears regularly and deals with a particular subject or is written by a particular writer

- the left-hand column

- a column of text

  

- sitizen noun.

- When you're old, people treat you like a second-class citizen.

  
  

- ordinary

- normal or average, and not unusual or special

- It was just an ordinary Saturday morning.

- an ordinary sort of day

- sort

- a group or type of people or things that are similar in a particular way

- sort of somebody/something ‘What sort of music do you like?’ ‘Oh, all sorts.’

- a particular type of person

- My brother would never cheat on his wife; he's not that sort.

  

- investigate \ in-ˈve-stə-ˌgāt

  
  

- emerge

  

- pattern

- noun.

- she stared at a flower pattern on the wall.

  

- a series of actions or events that together show how things normally happen or are done

- Patterns of employment in urban areas are different from those in the countryside.

  
  

- employment

- the state of being employed or having a job

- the occupation for which you are paid


## 4.7
句子 
https://searchsentences.com/words/conformity-in-a-sentence
https://github.com/SpaceVim/SpaceVim/blob/master/docs/cn/documentation.md

- conformity \ kən-ˈfȯr-mə-tē
We must act in conformity with local regulations

significant 
Your work has shown a significant improvement.
The drug has had no significant effect on stopping the spread of the disease

 regulations

### 4.3
- exquisite \ ek-ˈskwi-zət 比较典型的发音，egs gui... s不变，k阻碍
- Her wedding dress was absolutely exquisite.

- sensitive
	- She is very sensitive to other people's feelings.

- debut \ ˈdā-ˌbyü
	- the first public appearance of a performer or sports player

	- He will make his debut for the first team this week.
- check-up
	- an examination of somebody/something, especially a medical one to make sure that you are healthy

    to go for/to have a check-up
- check up on 
	- to make sure that somebody is doing what they should be doing
		- My parents are always checking up on me.

	- to find out if something is true or correct
		- I need to check up on a few things before I can decide.

- remarkable \ ri-ˈmär-kə-blē
	- unusual or surprising in a way that causes people to take notice
	-  The area is remarkable for its scenery.
		- scenery \ ˈsē-nə-rē

- extent
	- how large, important, serious, etc. something is
	- We don't know the extent of his injuries at this point.

- break
	- to stop doing something for a while, especially when it is time to eat or have a drink
		- break for something Let's break for lunch.

- catch up
	1. to reach the same level or standard as somebody who was better or more advanced
	- After missing a term through illness, he had to work hard to catch up with the others.

- advanced \ əd-ˈvan(t)st 注意发音 tst
	1. having the most modern and recently developed ideas, methods, etc.
	- Sweden has a reputation for advanced and stylish design.


- break
	1. to stop doing something for a while, especially when it is time to eat or have a drink
	- break for something Let's break for lunch.

一个有价值的问题，包含于另一个有价值的体系。所以我找到了youtube 
channel: Gerry English Expressions
"Speaking like a native speaker - t to d (flap t) - N. American Pronunciation"


https://membean.com/treelist

## search engine
类似网站
https://spymetrics.ru/en
http://www.topsimilarsites.com/

[查英语很好](https://www.wolframalpha.com)
[boardreader牛逼](https://boardreader.com)
[ecosia](https://www.ecosia.org/)
[mojeek](https://www.mojeek.com)
[discretesearch](https://www.discretesearch.com)
[search.carrot2.org](https://search.carrot2.org)
[searchencrypt](https://searchencrypt.com/)
http://www.thesearchenginelist.com/


[kartoo](http://www.kartoo.com/)

[search.myway](https://search.myway.com)

[lycos](http://www.lycos.com/)

[yippy](https://www.yippy.com/)

### 导航
[alvista](https://alvista.com/)


### 4.2
electricity \ i-ˌlek-ˈtri-sə-tē t阻碍
chemical  \ ˈke-mi-kəl  k 阻碍
alternative \ ȯl-ˈtər-nə-tiv t阻碍
surgical \ ˈsər-ji-kəl k 阻碍
vehicle \ ˈvē-ə-kəl  k阻碍
priority \ prī-ˈȯr-ə-tē t 阻碍

american \ ə-ˈmer-ə-kən 阻碍 , 也可不阻碍


发音新规则，3音节，非重音，似乎看第二个音节的r有关，无辅音，则扮演有的角色，不阻碍，其余形式同2音节规律，反正鉴定，3音节还是和前面有关，不与第一挂钩，虽然部分人会挂钩。

- century noun. \ ˈsen(t)-sh(ə-)rē 注意发音 (t)-sh 成
- somewhat
	- to some degree
	- I was somewhat surprised to see him.

- motive \ ˈmō-tiv noun.
	-  a reason for doing something

	- There seemed to be no motive for the murder.

- desire \ di-ˈzī(-ə)r noun.
	- a strong with to have or do something
		- He now had enough money to satisfy all his desires.

- satisfy
	-  to provide what is wanted, needed or asked for
		- The food wasn't enough to satisfy his hunger.
		- The education system must satisfy the needs of all children.

- announcement \ ə-ˈnau̇n(t)-smənt
	- noun.
	- a spoken or written statement that informs people about something
		- We welcome the recent announcement by the Government.

- inform 
	- to tell somebody about something, especially in an official way

- defeat
	- failure to win or to be sueecssful
		- failure: The success or failure
	- They suffered a narrow defeat in the final.
		- narrow
			- only just achieved or avoided
			- a narrow victory

- 纠正发音

- maintain \ mān-ˈtān

- sceond \ ˈse-kənd k阻碍

- assurance \ ə-ˈshu̇r-ən(t)s 遇到ce ts连读

- notification  \ ˌnō-tə-fə-ˈkā-shən noun.
	- official information of something; the act of giving or receiving this 

information
		- You should receive (a) notification of our decision in the next week.	
		- decision \ di-ˈsi-zhən m-w音标不准。。

- profit \ ˈprä-fət
- benefit \ ˈbe-nə-ˌfit  中介，重音部分i音标变为i 非重音自然嘴型，似乎3音节更需要，可能次重音和词源有关

- admit \ əd-ˈmit
	- verb.
	- to agree that something is true, especially when you are unhappy, sorry, or surprised about it
	- Why don't you just admit defeat (= recognize that you cannot do something) and let someone else try?


https://www.investopedia.com/terms/p/profit.asp
https://blog.talaera.com/business-emails-phrases
google 提问的思路
http://www.learnersdictionary.com/qa/how-are-you-in-an-email

不错的学习
https://elt.oup.com/?cc=us&selLanguage=en
https://www.grammarly.com/blog/i-hope-youre-doing-well/
https://www.businesswritingblog.com/business_writing/2012/07/opening-sentences-for-global-email.html



提出正确的问题比得到正确答案更重要
https://www.hbrchina.org/2018-03-12/5924.html#
https://www.zreading.cn/archives/5585.html
这三个场景里，提问比答案重要[提问篇2] - 小王的文章 - 知乎
https://zhuanlan.zhihu.com/p/108417362
https://blog.just4fun.site/post/%E5%B0%91%E5%84%BF%E7%BC%96%E7%A8%8B/asking-the-right-question-is-more-important-than-getting-the-right-answer/
英文引用
https://lemire.me/blog/2018/12/06/asking-the-right-question-is-more-important-than-getting-the-right-answer/

因此，要找到好的问题，你必须与材料保持一定距离。如果你认为我将“好问题”定义为“秘密”或“高度原创”的问题，这应该是没有争议的。

我们的思维倾向于根据我们学到的模式来构建一切。花两年时间学习马克思主义，每一个问题对你来说都会成为马克思主义的问题。你很难在框架之外提出新的问题。

不要误会我的意思：聪明的人往往更有创造力，其他一切都是平等的……但是，在知识渊博和被锁在思维的框架里之间存在差异。

## key: 对我来说一个重要的词:  思想枷锁

我们怎么能问更好的问题呢？

    注意周围的事物并改变你的世界观(看待世界的方式)。弗莱明(Fleming)是如何发现青霉素的？他注意到一些侵入他肮脏的实验室的霉菌似乎会杀死细菌。他当时问了正确的问题。
    耐心点。据报道，爱因斯坦曾经说过，“并不是我多聪明，只不过是因为我在问题里待了更久。” 你在一个问题上花的时间越长，就越有可能找到有趣的问题。（参见Forthmann et al. 2018）错过这些重要问题的最简单方法是将它们视为无趣的并且继续过快前进。
    保持身体活跃，去散步。将自己束缚在桌子上可能会适得其反。我曾经认为，作为一个全力以赴的知识分子是最好的路线，但我现在相信我是非常错误的。我平日几乎每天早上都在外面散步。（见Oppezzo and Schwartz，2014）。
    不要太社交。对顺从的社会压力会引发强烈的本能反应。对抗牛群是艰难的。因此，你最好不要过多地了解牛群的位置。具体而言，花几天独处。 Bernstein et al.（2018）建议间歇性的社交互动，而不是持续的互动，以避免个人探索的减少。
    多问问题。如果你想善于提供正确的答案，训练自己多回答问题。如果你想善于提问，那就多问问题。
    总是质疑自己的想法和工作。


### 4.1
http://www.kidsenglishbooks.com/sleepingbeauty
https://www.fluentu.com/blog/english/english-children-books/

## child’s language skills

As is with his other [developments](http://babyinsider.net/category/baby-development/), you can’t rush your baby’s speech. However, the following tips will help him develop it the right way.

-   Tell him what is happening around him throughout the day.
-   Tell and read a lot of stories to him.
-   Use real words when referring to objects to help him remember those.
-   Follow your child’s lead and talk about the objects that interest him.
-   Take him outside often to expand what he sees and his vocabulary.
-   Give him songs to listen to.
-   Give him positive feedback.
- 
kids crosswor book

原来有很多东西，阅读，语音，只是很小，太小一块了。
https://www.bestappsforkids.com/ 

## 规律
一、 记忆规律（次量原理）
人类的记忆跟你花的时间没有关系，是跟你打交道的次数有关系，通过科学研究发祥，跟一个字打交道165次左右，就可以终生不忘，这就叫做记忆的次量原理。
应该同一个事物165次吧

语言是习得的，不是死记硬背知识点学会的

自古以来，我们的古人就是直接学唐诗宋词，诸子百家，经史子集的。文化和智慧的东西都学会了，语言说话顺便就学会了。相反很长时间都在学一些肤浅的东西，是在大量的浪费孩子的时间、能力和智慧。

第四，光学几句干巴巴的英文不行。不要总是把阅读的目的放在提高英文上，阅读首先是吸收知识，吸收知识的过程中自然而然就吸收了语言。
感觉就像吃饭吃菜，分开就难，很神奇，合理组合，达到最好的状态

王佐良

通过文化来学习语言

通过文化来学习语言，语言也会学得更好。

语言之有魅力，风格之值得研究，主要是因为后面有一个大的精神世界：但这两者又必须艺术地融合在一起，因此语言表达力同思想洞察力又是互相促进的。

文体，风格的研究是有实际用途的，它可以使我们更深入地观察英语的性能，看到英语的长处，短处，以及我们在学习英语时应该特别注意或警惕的地方。因为英语一方面不难使用，一方面又在不小心或过分小心的使用者面前布满了陷阱。

此处感觉禅意十足

要理解一国的文化就要读些历史，文学，包括诗和散文作品。我国古时儿童入私塾读书，开始读《三字经》，《千字文》，《百家姓》，此外还要读《千家诗》或《唐诗三百首》，也就是要蒙童及早地接触我国传统文化的意思

多一点理解，了解更前面的东西，或许对现在才会豁然开朗。进化关系，所以看看美国经典，传统 ，更前的作品

简易读物对打好基础极有用，要多读。一是数量要多，至少读四十本。

“精读”和“泛读
当我看到这个的时候，我知道了，道理差不多，但是不同语言有他固有的东西，只能一切从他里面寻找。不能用中文的思维来指导，这样又错过了英文的机会，每次都是错过最重要的机会。

作者：WinKey英启在线英语
链接：https://www.jianshu.com/p/689e2a0a1a05

- stuff
	- This wine is good stuff.

- stick
	- Her wet clothes were sticking to her body.

- sticky
	- made of or covered with a substance that stays attached to any surface it touches: 
	- The dough should be soft but not sticky.

### kids english learning

## words
- sort
- He's the sort of person who only cares about money.

- variety (of something) 
- several different sorts of the same thing
- This tool can be used in a variety of ways.

- form
	- a type or variety of something
	- Swimming is one of the best forms of exercise.

	-  the particular way something is, seems, looks or is presented
	- The disease can take several different forms.

	- to make or be something
	- This information formed the basis of the report.

- individual
	- a person considered separately rather than as part of a group
	- There is no single individual who is to blame.

## 发音纠正
- particular \ pər-ˈti-kyə-lər 发音纠正

- variety \ və-ˈrī-ə-tē 发音纠正 t也可以发阻碍，可能因为第二音节没有辅音，导致t算第二个，ī-ə 算一个元音组合了

##phrase
A Huge Thanks


english news:
https://www.sciencedaily.com/



### 3.31
A negative sentence or phrase is one that contains a word such as "not", "no", "never", or "nothing":
"I've never seen him in my life" is a negative sentence.

capability
These tests are beyond the capability of an average twelve-year-old.

authority \ ə-ˈthȯr-ə-tē t的发音在对th的理解，如果偏向出气就是t,偏向少气，t发d亦可
今天才知道这么久的发音，不仅为了自己，也是为了更好的解决听力问题。谢谢

dictionary \ ˈdik-shə-ˌner-ē 以后作为典型发音n n 

whatsoever \ ˌ(h)wät-sə-ˈwe-vər t略读，s后面ə 发ou，不解，可能是自然连读产生的。
importance \ im-ˈpȯr-tᵊn(t)s t可发阻碍或稍微明显点的d，后一个(t)和s相连，以前以为是不用读，现在才知道是和s连读ts

preventing \ pri-ˈvent forvo发音，很完美验证了t的2音节规律 
m r / l n 这个挺重要的分类
written \ ˈri-tᵊn 不用怀疑，质疑经验t确实阻碍到和n同化了，rin
https://www.zhihu.com/question/20165553
今天想了一个胆量，问题，居然看到马云，我不昨晚刚看吗，还有
斯蒂芬·克拉申(Stephen D. Krashen)的第二语言习理论，我不刚看完没多久吗。
一个有价值的问题，有人能够这样去看，要学习。
突然想到KPI，很重要...
《学会提问》《批判性思维》《批判性思维工具》《好好讲道理》《孙子兵法》



### 3.30

能查看各种包在各种发行版的软件
https://pkgs.org/
https://repology.org/project/fcitx-table-extra/versions
能看到上游:https://packages.aosc.io/packages/fcitx-table-extra

查单词网站
https://www.wordreference.com/definition/
https://www.englishlearner.com/
https://www.wordwebonline.com/

https://www.2daygeek.com/category/linux-commands/

- author \ ˈȯ-thər th是ð 美音里th θ 都部分音标显示的

- exit \ ˈeg-zət

- synopsis \ sə-ˈnäp-səs p阻碍，注意发音
- a short description of the contents of something such as a film or book

- execute \ ˈek-si-ˌkyüt k也阻碍，s正常，注意发音
- to make a [computer](https://dictionary.cambridge.org/dictionary/english/computer "computer") [program](https://dictionary.cambridge.org/dictionary/english/program "program") or [instruction](https://dictionary.cambridge.org/dictionary/english/instruction "instruction") [work](https://dictionary.cambridge.org/dictionary/english/work "work"):

- routine
a usual or fixed way of doing things:
There's no set/fixed routine at work - every day is different.

- punish
- to cause someone who has done something wrong or committed a crime to suffer, 

- suffer
- to experience physical or mental pain:
I think he suffered a lot when his wife left him.

总结一个音节，气出完，需要阻碍，元音末尾，几乎是阻碍，轻声的。

the door through which you might leave a building or large vehicle, or the act of leaving something, especially a theatre stage: 

- miscellaneous  \ ˌmi-sə-ˈlā-nē-əs
- consisting of a [mixture](https://dictionary.cambridge.org/dictionary/english/mixture "mixture") of [various](https://dictionary.cambridge.org/dictionary/english/various "various") things that are not usually [connected](https://dictionary.cambridge.org/dictionary/english/connected "connected") with each other:


- library  \ ˈlī-ˌbrer-ē 
- a building, room, or organization that has a collection, especially of books, for people to read or borrow, usually without payment

- convention
- a large formal meeting of people who do a particular job or have a similar interest, or a large meeting for a political party: 
- the national Democratic convention

- prisoner \ ˈpriz-nər 注意发音，n确实承前启后

### 3.28

larry selinker 石化现象

http://blog.sciencenet.cn/home.php?mod=space&uid=39731

"word" + news / article 去寻找或直接google里建议查找经典的词

这词典有意思
https://www.mathsisfun.com/definitions/deviation.html
http://www.businessdictionary.com/definition/deviation.html

- deviation  \ ˌdē-vē-ˈā-shən
- a variation that deviates from the standard or norm
- center \ ˈsen-tər UK centre
- She's the centre of attention everywhere she goes.
 Standard Deviation vs. Average Deviation


- REMOTE
- They live in a remote corner of Scotland, miles from the nearest shop.

- review
- Please rate and review your purchase on our website.
-to look again at something you have studied, especially in order to prepare for an exam

- semester \ sə-ˈme-stər 
- one of the periods into which a year is divided at a college or university, especially in the US and Australia:
the first/second semester

- college
- a university where students can study for a degree after they have left school
- She's now in her first year of college.

- university -- \ ˌyü-nə-ˈvər-sə-tē 注意发音ə后面发,i ，其他不变

- qualification -- \ ˌkwä-lə-fə-ˈkā-shən 都是ə
- an official record showing that you have finished a training course or have the necessary skills, etc.:
You'll never get a good job if you don't have any qualifications.
-  an exam that you have passed or a course of study that you have successfully completed

    academic/educational/professional/vocational qualifications

- activity
-  a thing that somebody does in order to achieve a particular aim

    criminal/terrorist/illegal activities

- squash \ ˈskwäsh
- to push yourself, a person, or thing into a small space:
The room was so full you couldn't squash another person in.
-  We all squashed into the back of the car.
- The tomatoes at the bottom of the bag had been squashed.

- crush 
- The car was completely crushed under the truck.
-  to press something so hard that it is damaged or injured, or loses its shape

- hard
- Ooh, you're a hard woman, Elaine!

- gentle
- calm, kind, or soft; not violent or severe: 

- severe
- extremely bad or serious

    His injuries are severe.
- severe weather/storms

- steep 
- rising or falling quickly, not gradually

    a steep hill/slope
    a steep climb/descent/drop
    a steep flight of stairs

- informal. He wants to move in here with us? That’s a bit steep!

- climb \ ˈklīm 注意b，不发音 verb.

- noun. an act or process of climbing: 
- We were very tired after our climb.
- It's a steep climb to the top of the mountain, but the view is worth it.

- violent
- The more violent scenes in the film were cut when it was shown on television.
- He yells a lot but I don't think he's ever been physically violent towards her.

- event \ i-ˈvent 

- yell 
- The child yelled out in pain.

- essential \ i-ˈsen(t)-shəl
- connected with the most important aspect or basic nature of somebody/something synonym fundamental

    The essential difference between Sara and me is in our attitude to money.
- an essential element/ingredient/component of something

- as if/ as thogh
- in a way that makes it seem that something is true or that something is happening
- said to show that you do not believe something is possible:
"Did you get a raise?" "As if!"


### 3.27 
- polish \ ˈpä-lish
to rub something using a piece of cloth or brush to clean it and make it shine:

https://www.mingyantong.com/tags/22813

- bother
- to make the effort to do something: 
- to spend time and/or energy doing something

    ‘Shall I wait?’ ‘No, don't bother’.
- I don't know why I bother! Nobody ever listens!

- to make someone feel worried or upset:
Does it bother you that he's out so much of the time?

- effort
- an attempt to do something especially when it is difficult to do
- Please make an effort to be on time.

- affort -- \ ə-ˈfekt

- effort -- \ i-ˈfekt

Affect is usually a verb, meaning to influence or act upon. 
Effect is usually a noun, meaning the result of an action.


- outbreak 
- a sudden appearance of something, esp. of a disease or something else dangerous or unpleasant:
- an outbreak of cholera
- the outbreak of war
http://www.finedictionary.com

https://www.englishpractice.com/topics/common-mistakes/page/2/

https://www.thoughtco.com/esl-4133095

https://pronuncian.com/

http://www.antimoon.com/
https://thesoundofenglish.org/audio/

the sound of english pronunciation

ex-在词首有三种发音：［igz］［iks］或［eks］

基本规律是：

1.以“ex”开头的单词，不管其后为何音素，只要第一个音节为重读或次重读的，“ex”发［eks］
2.以“ex”开头的单词，其重音落在第二个音节上，且其后为元音音素的，“ex”发［igz］
3.以“ex”开头的单词，其重音落在第二个音节上，且其后为辅音音素的，“ek”发［iks］


explanation
\ ˌek-splə-ˈnā-shən

- pronounce --\ prə-ˈnau̇n(t)s
- The ‘b’ in lamb is not pronounced.
- I hesitate to pronounce judgement in such a case.

- tongue --\ ˈtəŋ noun. verb. 

- vowel --\ ˈvau̇(-ə)l
- a letter that represents a sound produced in this way:
The vowels in English are a, e, i, o, and u.
- a speech sound produced by humans when the breath flows out through the mouth without being blocked by the teeth, tongue, or lips:
A short vowel is a short sound as in the word "cup".
A long vowel is a long sound as in the word "shoe".

- consonant --\ ˈkän(t)-s(ə-)nənt
- a speech sound produced by human beings when the breath that flows out through the mouth is blocked by the teeth, tongue, or lips


- speech
the language used when talking:
Some expressions are used more in speech than in writing.

- flow
- to move in one direction, especially continuously and easily: 
- Many short rivers flow into the Pacific Ocean.

- swallow
- to cause food, drink, pills, etc. to move from your mouth into your stomach by using the muscles of your throat: 

- flesh
- The soft part of the body of a person or animal that is between the skin and the bones, or the soft inside part of a fruit or vegetable

- adverb
- a word that adds more information about place, time, manner, cause or degree to a verb, an adjective, a phrase or another adverb

    In ‘speak kindly’, ‘incredibly deep’, ‘just in time’ and ‘too quickly’, ‘kindly’, ‘incredibly’, ‘just’ and ‘too’ are all adverbs.

### 3.26
比如experience 这个词，要理解，就必须会从句子中提炼
the things that have happened to you that influence the way you think and behave

-   Experience has taught me that life can be very unfair.
- 
the knowledge and skill that you have gained through doing something for a period of time; the process of gaining this

    My lack of practical experience was a disadvantage. \ ˌdis-əd-ˈvan-tij
    
解释帮你找一条路线，大致的轮廓
例句帮你找到这个词的感觉，所包含的内涵
一定要根据例句，找到画面感，不能靠想象。1个肯定不够，至少3个对比过，来找到，对比，确定他的真正内涵。
必须在茫茫中找到最真的那个，而不被干扰

https://baike.baidu.com/item/%E5%A4%A7%E5%AD%A6%E4%B8%93%E4%B8%9A/3632681

noun [singular] (informal) Idioms synonym countable, uncountable "Word Family" (in adjectives) topics

产品分析http://www.woshipm.com/
mechanical 
The plane appeared to have crashed because of a mechanical problem.
without thinking about what you are doing, especially because you do something often:
He gave a mechanical response.


mechanics
the particular way something works or happens:
the goals are the same, but the mechanics for achieveing the goals differ greatly.

physically 
Special holidays are available for physically handicapped/disabled people (= those lacking the full use of part of their body).

AVAILABLE
If someone is available, the have enough time to do something.
Are you available Thursday morning for for a conference call?

differ
The twins look alike, but they differ in temperament.

universe --\ ˈyü-nə-ˌvərs ə基本是i,发ə也不错，看习惯和个人表达
the whole of space and everything in it, including the earth, the planets and the stars

temperament --\ ˈtem-p(ə-)rə-mənt 根据规则，确实p是b
a person’s or an animal’s nature as shown in the way they behave or react to situations or people

    to have an artistic temperament


conservation
the protection of the natural environment
to be interested in wildlife conversation

nature
the usual way that a person or an animal behaves that is part of their character

usual
that happens or is done most of the time of in most cases


qualified
having passed the exams or completed the training that are necessary in order to do a particular job; having the experience to do a particular job
a qualified teacher/doctor

### 3.25
- compression
the act of pressing something into a smaller space or putting pressure on it from different sides until it gets smaller:

- decompressive \ ˌdē-kəm-ˈpres-iv

- decompress
To relieve of pressure or compression.
to make an unpleasant feeling, such as pain or worry, less strong:
She was given a shot of morphine to relieve the pain.

linux学习网站
https://www.guru99.com/file-permissions.html
https://opensource.com/article/19/6/understanding-linux-permissions
https://opensource.com/article/19/8/understanding-file-paths-linux
https://opensource.com/article/19/3/move-your-dotfiles-version-control
https://www.linux-laptop.net/

学习，英语，论文 相关
https://www.lunwenspace.com/m/view.php?aid=4178

朱陆之辩研究综述
https://www.sinoss.net/uploadfile/2010/1119/20101119101947411.pdf


单词对比网站，有图片
https://www.askdifference.com/cereal-vs-grain/

- characterization --\ ˌker-ik-t(ə-)rə-ˈzā-shən 听多遍发现i偏向ə,后面ə是对的，因为第一次误听成i
- the way that people are represented in a film, play, or book so that they seem real and natural:
The plots in her books are very strong but there's almost no characterization.
The film's characterization of the artist as a complete drunk has annoyed a lot of people.
the way that a writer makes characters in a book or play seem real

    a work of comic brilliance and masterly characterization

- a description of the most typical or important characteristics of someone or something:
I don’t agree with your characterization of my home town as a boring place to live.


- bran --\ ˈbran 糠
- the outside of the grain of a cereal such as wheat or oats
	- grain
	- the seeds from crops such as wheat, rice, or barley that are used for food
		- seed
		- a small hard part produced by a plant that can grow into a new plant of the same type

		- crop --\ ˈkräp
		- a plant that is grown in large quantities, especially as food
			- food crops

		- barley
		- a plant that produces grain used for making food, beer, and whisky

		- wheat
		- a tall plant that produces grain for making bread and other foods

		- oat \ ˈōt
		- grain grown in cool countries as food for animals and for making flour, porridge, etc.

		- cereal
		- one of various types of grass that produce grains that can be eaten or are used to make flour or bread. wheat, barley and rye are all cereals
		- A grain used for food, such as wheat, oats, or corn
		- a food that is made from grain and eaten with milk, especially in the morning

- nerve
- a group of long, thin fibres (= structures like threads) that carry information or instructions between the brain and other parts of the body:

- the courage or confidence necessary to do something difficult, unpleasant, or rude
- She was a bundle of nerves (= very nervous) before the audition.

- audition \ ȯ-ˈdi-shən
- a short performance given by an actor, a singer, etc., so that somebody can decide whether they are suitable to act in a play, sing in a concert, etc.


### 3.24
词典https://findwords.info/term/
https://www.abbreviations.com
https://www.spellzone.com/dictionary/
https://diffsense.com/diff
https://topmeaning.com/english

- breadth --\ ˈbretth
the distance from one side to another

- monospaced --/ˈmɑː.noʊ/
 (Printing, Lithography & Bookbinding) (of printed material) having been printed in a font in which all characters have the same breadth

- confusion -- \ kən-ˈfyü-zhən
To avoid confusion, the twins never wore the same chothes.

- emphasize --\ ˈem(p)-fə-ˌsīz
To give special importance to sth.
The report emphasizes the need for economic stability.

- disorder
an untidy state

- 帧率英文为Frame Rate，单位Frame Per Second（FPS），某些情况简称FPS，指视频每秒包含的帧数。
视频帧率最低设置为24帧，这和人眼的反应速度有关，当帧率低于这个数值时，人眼就会感觉到明显的卡顿。

通常视频的帧率设置为30FPS，

- 比特率，英文为Bit Rate，是指每秒传送的比特(bit)数。[1]
单位为bps(Bit Per Second)
比特率越高，传送的数据越大
在视频领域,比特率常翻译为码率
比特率是影响视频清晰度的一个重要参数
比特率决定了视频大小 
当比特率越大，视频清晰度就越高。其影响存在边际效应递减现象，并且存在上限（视频原始数据的画质）

https://blog.csdn.net/benkaoya/article/details/79558896
网上这篇文章「Video Encoding Settings for H.264 Excellence」，就针对H.264视频编码，测试了不同视频分辨率下的码率阈值。
http://www.lighterra.com/papers/videoencodingh264/

分辨率/2.8 就是建议码率 M/S

不错的词典
http://www.finedictionary.com/durra.html

https://www.wordnik.com/

medical词典
http://meddict.org/
http://www.irishhealth.com/search.html
https://www.healthdictionary.org/

retiree
a person who has stopped working in regular paid employment because of their age

- invest
You have all invested significant amounts of time and energy in making this project the success that it is.

- severe
 If the pain becomes severe, you may wish to contact a doctor.
severe learning difficulties

- among --\ ə-ˈməŋ

- place
to put something in a particular position: 

- disengage --\ ˌdis-in-ˈgāj 注意发音，s不需要按规则，原音
to become physically separated from something, or to make two things become physically separated:
The door was disengaged from one of its hinges.

- perform
to do an action or piece of work:
Computers can perform a variety of tasks.
to entertain people by dancing, singing, acting, or playing music

- dramatic -- \ drə-ˈma-tik 
sudden, very great and often surprising
There has been a dramatic rise in reported crime.

- plunge
move or fall suddenly and often a long way forward, down, or into something:
We ran down to the beach and plunged into the sea.


### 3.23

https://linux.cn/article-11422-1.html

这词典不错，还有视频https://www.englishlearner.com/dictionary/

https://www.wordsmyth.net/

近义词
https://www.macmillanthesaurus.com/


https://www.latin-is-simple.com/en/vocabulary/phrase/1656/

https://www.thoughtco.com/history-and-culture-4133356

- fibreglass
a strong light material made from glass [fibres](https://www.oxfordlearnersdictionaries.com/definition/english/fibre#fibre_topg_1 "fibres definition") and plastic, used for making boats, etc.

- repose
a [calm](https://www.macmillandictionary.com/us/dictionary/british/calm_1 "calm") or [relaxed](https://www.macmillandictionary.com/us/dictionary/british/relaxed "relaxed") [state](https://www.macmillandictionary.com/us/dictionary/british/state_1 "state")

- requiescat -- \ ˌre-kwē-ˈe-ˌskät

- playback
the use of a machine to show pictures or play sounds that were recorded earlier

We recorded the show for later playback.

- continuous
continuing without stopping or being interrupted

a continuous flow of water

- the continuous movement of a line of vehicles or people

The new system should speed up the traffic flow.

- a substance that can flow, has no fixed shape, and is not a solid or a gas

a glass of colourless liquid

The detergent is available as a powder or a liquid.

- fluid (注意sepecially a liquid)
A substance that has no fixed shape and yields easily to external pressure; a gas or (especially) a liquid.
‘we all need several glasses of fluid a day’

- reversal
A substance that has no fixed shape and yields easily to external pressure; a gas or (especially) a liquid.
‘we all need several glasses of fluid a day’

- marked
clear and noticeable

- steady
Firmly fixed, supported, or balanced; not shaking or moving.

词典 http://foldoc.org/
比如PERM 是permission

- MANDATORY -- \ ˈman-də-ˌtȯr-ē
In 1991, the British government made it mandatory to wear rear seat belts in cars.
Mandatory arguments to long options are mandatory for short options too.

- PRESERVE -- \ pri-ˈzərv
to preserve the environment

PRESERVE VS PROTECT

protect: (1) to keep someone or something safe from harm, damage, or illness
(2) to help the industry and trade of your own country by taxing or restricting foreign goods

preserve: (1) to save something or someone from being harmed or destroyed.
e.g., We must encourage the planting of new trees and preserve our existing woodlands

- INTERACTIVE
An interactive system or computer program is designed to involve the user in the exchange of information:
an interactive game/video

involving communication between people:
interactive teaching methods

- VERBOSE --\ (ˌ)vər-ˈbōs 
using or containing more words than are necessary:
a verbose explanation/report/speech/style

- CURVE 
a line that bends continuously and has no straight parts: 

- PERM --\ ˈpərm
A hairstyle produced by setting the hair in waves or curls and then treating it with chemicals so that the style lasts for several months.


## 3.21
英语论坛https://forum.wordreference.com/forums/english-only.6/

reserve
investigation investigator
qualification
distincion
utilized
well-being
cotage
extent
sort of
manner
ideal
informal
expert

extravagant --\ ik-ˈstra-vi-gənt i确实都是ə的音
```
affinity --\ ə-ˈfi-nə-tē 符合2音节爆破音规律tt
A spontaneous or natural liking or sympathy for someone or something.
‘he has an affinity for the music of Berlioz’

attractive --\ ə-ˈtrak-tiv kt当成1个略读配上一个浊化阻碍音，属于1个辅看待

associated -- \ ə-ˈsō-shē-ˌā-təd 最后发音dit

painting -- \ ˈpān-tiŋ m-w是阻碍的，但是forvo是符合规律的

priority -- \ prī-ˈȯr-ə-tē m-w 不符合，forvo完全符合3音节规律，所以音标也是有区域标准的
```
cease --\ ˈsēs
to stop something:
Whether the protests will cease remains to be seen.
The company has decided to cease all UK operations after this year.

https://www.infoq.cn/
https://golangdocs.com/
https://www.golang-book.com/books/intro
https://www.codecademy.com/learn/learn-go
https://www.codecademy.com/learn/learn-go

查看网络服务
journalctl -bu NetworkMananger.service

udiskie
kde可能有kio这样的，属于kf5，所以kf5必装
kdenetwork-filesharing: Windows File and printer sharing for KDE，所以

### kf5
### kdebase
### kdesdk
### kdeutils
### kdenetwork必装(kdenetwork-filesharing  	kio-extras krdc krfb signon-kwallet-extension	zeroconf-ioslave)

- kdegraphics


### 3.20
转战98五笔

https://wubi98.gitee.io/download/2019/01/01/001.98wb.html
https://github.com/yanhuacuo/98wubi-tables
http://98wb.ys168.com/
http://www.98wubi.com/
http://www.aardio.com/

词源网站
https://onelook.com/?w=climatology&ls=a
https://rhymezone.com/r/d=-ology
https://wordinfo.info/results?searchString=climatology
https://www.wordsmyth.net

类似网站
google搜索 related:nospace.com
https://siteslike.com
https://www.similarsites.com/
https://www.similarweb.com
https://www.similarsitesearch.com
https://www.findsimilarsites.com
https://spymetrics.ru/en
http://www.topsimilarsites.com/

这个不错的搜索,比如搜索archlinux install
http://www.kartoo.com/

in charge of
responsible for something or someone:
Who’s in charge here?
The teacher put me in charge of organizing the project.
charge of:
There is a charge of £50 if you are over a week late with your payment.
charge for:
There is no charge for using the library.

moderator
someone who is in charge of a discussion, meeting etc between people with different opinions

mental
Stress can affect both your physical and mental health.
It is clear that mental activity does not stop when we’re asleep.

disorder
a state of untidiness or lack of organization:
The whole office was in a state of disorder.

untidy
Not arranged neatly and in order.
‘the place was dreadfully untidy’

psychology
The mental characteristics or attitude of a person or group.

prisoner
a person who is kept in prison as a punishment: 

punish
to cause people who have done something wrong or committed a crime to suffer by making them do something they don’t want to do or sending them to prison:
She was punished for being late to school.

conscious --\ ˈkän(t)-shəs注意tsh形成ch
to notice that a particular thing or person exists or is present:
My tooth doesn't exactly hurt, but I'm conscious of it (= I can feel it) all the time.

congition
the use of conscious mental processes: 

### 3.19
http://man7.org/linux/man-pages/index.html
https://www.freebsd.org/cgi/man.cgi?manpath=
https://www.manpagez.com/man/
http://man.he.net/
https://helpmanual.io/
https://freeze.sh/
https://sarata.com/manpages/
https://www.tutorialspoint.com/unix_commands/
https://ss64.com/bash/
https://linux.die.net/man/
http://linuxcommand.sourceforge.net/index.php
http://www.skrenta.com/rt/man/
https://www.ner2.com/category/linux/
https://www.systutorials.com/docs/linux/man/
https://ftp.gnu.org/old-gnu/Manuals/coreutils-4.5.4/html_chapter/coreutils_30.html#SEC187

https://linux.cn/article-10355-1.html
https://www.linux.org/

### 3.18
https://www.bbc.co.uk/learningenglish/oromo/course/english-you-need/unit-1
Unit 1: English You Need
Exams, news, pronunciation, teachers' tips, learners' questions

论坛https://www.englishforums.com/English/
https://www.englishforums.com/English/GeneralEnglishVocabularyIdiom-Questions/Forum29.htm

看新闻，学英语单词
https://www.ul.com/news
https://www.msn.com/ 每个版块都值得看标题
https://www.cnbc.com/
https://www.kickstarter.com/
http://todaynews.com/business/
https://www.nbcnews.com/

propose \ prə-ˈpōz
to offer or suggest a possible plan or action for other people to consider
- She proposed a boycott of the meeting.

take part in
to be involved in an activit with other people.


boycott
to refuse to buy a product or take part in an activity as a way of expressing strong disapproval.
the union called on its members to boycott the meeting.

call on

activity --\ ak-ˈti-və-tē

constitution --\ ˌkän(t)-stə-ˈtü-shən
a set of basic rules and principles for an organization that control how it operates
Some members were proposing changes to the club’s constitution.

written --\ ˈri-tᵊn 注意发音i不再是write里的发音了 t适用规则，并且注意n

possible --\ ˈpä-sə-bəl s不变，说明，非爆破音不适用规则

proposal
a formal suggestion, plan, or idea, often a written one.
Management has made proposal to cap overtime.

revision --\ ri-ˈvi-zhən 
the process of changing, improving, or making additions to sth such as a plan, law, or piece of writing
He intends to undertake a major revision of the constitution.

cap
a limit on the amount of money that can be charged or spent in connection with a particular activity: 

charged
(of arguments or subjects) causing strong feelings and differences of opinion or, more generally, filled with emotion or excitement:
Abortion is a highly charged issue.
He spoke in a voice charged with emotion.

accuse
to say that someone has done something wrong or illegal: 

charge
to ask an amount of money for something, especially a service or activity: 
an official statement accusing someone of committing a crime.
He is now likely to face a murder charge.
She's been charged with murder.

commit
commit yourself
to express an opinion or to make a decision that you tell people about:
to do something illegal or something that is considered wrong:
He was sent to prison for a crime that he didn't commit.

quirk --\ ˈkwərk 这个没有被重音影响，所以似乎距离超过2就不算了

prominent
Important; famous.
‘she was a prominent member of the city council’

council --\ ˈkau̇n(t)-səl
a group of people elected or chosen to make decisions or give advice on a particular subject, to represent a particular group of people, or to run a particular organization: 

represent
to speak, act, or be present officially for another person or people:
They chose a famous barrister to represent them in court.

reserve
I reserve judgment on this issue (= I won't give an opinion on it now) until we have more information.

## 3.17
词典http://www.photo-dictionary.com/

a team had a string of 13 wins last season

i was confronted by a string of questions.

travel up

go up
- move upward

to be built

New office buildings are going up everywhere.

(British English, formal) to arrive at a university, especially Oxford or Cambridge, at the beginning of a term or in order to begin your studies
She went up (to Oxford) in 2008.

to go from one place to another, especially further north or to a city or large town from a smaller place

When are you next going up to Scotland?

trip up

moor
to tie a boat so that it stays in the same place:
We moored further up the river.
We moored the boat to a large tree root.

mooring
a place where a boat or ship is moored. 

construction
the work of building or making something, especially buildings, bridges, etc.:

structure
the way in which the parts of a system or object are arranged or organized, or a system arranged in this way: 

fasten --\ ˈfa-sᵊn

tie
to fasten something in a particular place using something such as rope

reconstructive --\ ˌrē-kən-ˈstrəkt ə重音
Reconstructive medical treatment involves changing the shape of part of a person's body, either because it has been badly damaged or to improve someone's appearance
After the accident, he underwent reconstructive surgery to rebuild his face.

undergo 
to experience something that is unpleasant or something that involves a change:
She underwent an operation on a tumour in her left lung last year.

## 3.16
conditional -- \ kən-ˈdish-nəl

subject
a thing or person that is being discussed, described, or dealt with

conversation
a talk between two or more people, usually a private and informal on

finite

clause
 a group of words that includes a subject and a verb, and forms a sentence or part of a sentence

definite
clearly decided and specific
We haven’t arranged a definite date for our visit yet.


https://mp3.pm/
https://www.dailywritingtips.com/

## 3.14
英语词典https://mnemonicdictionary.com/
https://www.wordgamedictionary.com/dictionary/word/

新闻网站 https://www.alternet.org/
https://www.wikinews.org/

unbiased -- \ ˌən-ˈbī-əst
fair in the way that you describe or treat a situation

able to judge fairly because you are not influenced by your own opinions:

denote -- to mean something
The red sign denotes danger.
- tobe a sign
- A very high temperature often denotes a serious illness.

form -- 
- a type of something
- The car is by far the most popular form of transport.

belligerent -- \ bə-ˈlij-rənt
If someone is belligerent, they're eager to fight
unfriendly and aggressive
[only before noun] (formal) (of a country) fighting a war the belligerent countries/states/nations

specify --
to explain or describe something clearly and exactly: 
Please specify the dimensions of the room.

as
- Used in comparisons to refer to the extent or degree of something.
- ‘go as fast as you can’

- preposition

    1Used to refer to the function or character that someone or something has.
    ‘it came as a shock’


extent --\ ik-ˈstent 最后t的不阻碍
- area or length; amount: 
 We don't yet know the extent of his injuries (= how bad his injuries are).
Rosie's teacher was impressed by the extent of her knowledge (= how much she knew).
The River Nile is over 6,500 6,5000 kilometres in extent (= length).

-the degree to which something happens or is likely to happen:
She had not realized the extent to which the children had been affected.

refer
to look at a book or similar record in order to find information and help: 
- refer to somebody/something (as something)
to mention or speak about someone or something
- to look at something or ask a person for information

boom --
a sudden increase in trade and economic activity; a period of wealth and success

indicate--
- to show, point, or make clear in another way: 
- to express an intention, opinion, or wish in an indirect way

vehicle --\ ˈvē-ə-kəl 阻碍
road vehicles include cars, buses, and trucks.

fare
the money that you pay for a journey in a vehicle such as a bus or train
train fares are going up again.

forward -- \ ˈfȯr-wərd 注意重音 adj.
towards the direction that is in front of you.
forward motion/movement

towards the future
i always look forward, not back.

progress v.
to improve or develop in skills, knowledge, etc.
My spanish never really progressed beyond the stage of being able to  orderdrinks at the bar.

- n.
- movement to an improved or more developed state, or to a forward position.
- I'm not making much progress my Spanish.

Technological progress has been so rapid over the last few years.
rapid -- \ ˈra-pəd 完全符合规则，p阻碍，ə不弱化，因为没有舌尖位置

## 3.12

demonym -- \ ˈde-mə-ˌnim
a word that is a name for someone who comes from a particular place:
The demonym for Spain is a Spaniard, not "a Spanish".
Pinoy is an informal demonym referring to Filipinos.

thefreedict 和definition这2词典不用

trip 
to lose your balance because your foot hits against something when you are walking or running, or to cause someone to lose his or her balance: 

rock
the hard solid substance that forms part of the Earth’s surface

triangular --\ trī-ˈaŋ-gyə-lər
shaped like a triangle: 

triangle 
a flat shape with three straight sides:

firm
trip 
footing

eng learning mind :https://www.zhihu.com/question/22447974/answer/1071742222
http://www.foryou.sg/wbn/slot/u401/cart/115cart5.htm
http://www.xindeng.org/baike/waiyu/fangfa/
http://www.charity.idv.tw/g/g.htm

单词维基
https://orthodoxwiki.org/
https://rationalwiki.org/wiki/
https://en.vikidia.org/wiki/

1．早期借用词--大陆时期

2．第二期借用词--古英语时期

3．第三期借用词--中古英语时期
中古时期对英语词汇影响最大的是法语，而法语属于罗马语族（又称拉丁语族），是由古拉丁语演变而来，属于拉丁语的分支，因此很难判定哪些词是英语直接从古拉丁语借来的，哪些词是通过法语进入英语的。

4．第四期借用词--文艺复兴之后
　　文艺复兴时期，欧洲学者们致力于对古典文化的研究。古典语言（拉丁语、希腊语）和古典文学成为教育的主要内容。从十六世纪到十八世纪，文学家、科学家都用拉丁语写论文，如培根（Francis Bacon）、牛顿（Isaac Newton, 1642--1727）的著作便是这样。
　　据《牛津大词典》的资料，在文艺复兴时期进入英语的外来词有一万二千个以上，其中绝大部分来自法语或拉丁语。这些词大多属于学术性的词汇，例如表示抽象概念的词和科技术语。英语词汇中大部分属于欧洲语言国际性成分的词全部源自这一批拉丁词。

-tion，-sion这些的都是拉丁语；-logy、th、ty这样的往往是希腊语。

[英语中拉丁比例](https://www.douban.com/note/250252677/)
世界语言谱系分类表](https://web.csulb.edu/~txie/CLERC/sjyypxflb.htm)
fb: 使用搜索手机常见问题，为潜在客户创建原始内容

pixel -- \ ˈpik-səl k不属于开头重音，所以k略读

how to install a pixel and set up a conversion ad
n属于气很多的音，t任然不少 以后有n 必出t

### con发音
condition -- \ kən-ˈdi-shən 注意发音o发ə

refusal n.
the act of refusing to do or accept sth
the act of saying that you will not do or accept something:
Her request for more money met with a refusal.

frustrated 
annoyed, disappointed, or discouraged:
You just get so frustrated when everything in your vegetable garden is ripe and then the bugs get at them.
feeling annoyed or less confident because you cannot achieve what you want:
Are you feeling frustrated in your present job?

either 
used in negatives instead of also or too:
The restaurant has good food, and it’s not expensive either.

one or the other of two
You can go by train or bus – either way it’ll take an hour.

negative  \ ˈne-gə-tiv 发t 遇到n似乎必出t
### 注意弱化 ə 成 i,次重音也是个标记
literature \ ˈli-tə-rə-ˌchu̇r 注意发音t浊化d ə弱化成i 似乎2音节单词很特殊，

## t规则 辅音和辅音就要延续，辅音和元音就要相对。
辅音在2音节以内无效，以元音为第一.

和前面是否重音没有关系，是否出气的辅音才有关，和前后直接接触的有关,尤其后面，辅音遇到元音，浊化最佳，
遇到n r 似乎必出t
l不出

舌头位置在前面就T : r n
舌头位置在后面就D : l b
舌头在前，几乎都出气，可以夸张的验证 
比如b 出气就是p 了，所以b不出

type of 根据个人理论 连续已经是讲前后当成一个词了，所以 typeof p前后是元音,并且在3音节以内(保证了辅音不起规则，元音优先)， 所以p 都是浊化
cup of 

计算机词典
 https://www.urbandictionary.com/
https://techterms.com/definition/
https://en.wiktionary.org/wiki/
https://www.computerhope.com/jargon.htm

新思路，eng-latin词典 https://glosbe.com/en/la/daemon
https://glosbe.com/en/la/{searchTerms}


## 3.11
看完福耀，国内税收要继续拓展的人生

ultimate -- \ ˈəl-tə-mət t发t 虽然符合各种规则，但是l出气了，所以继续t

wiki词条 familly planning

新闻https://bihu.com/
类似牛客https://leetcode-cn.com
算法工程https://blog.csdn.net/m0_37907797/article/details/102661778?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task
最后，很多人问我都是怎么学习的，那我干脆就把我看过的优质书籍贡献出来：

计算机基础入门推荐：《程序是怎样跑起来的》、《网络是怎样连接的》、《计算机是怎样工作的》

进一步认识计算机网络：《计算机网络:自顶向下》、《图解http》

数据结构+算法入门：《数据结构与算法分析：C语言描述版》，《大话数据结构》、《阿哈算法》

算法进阶：《算法第四版》、《编程之美》、《编程珠玑》

由于我是Java技术栈的，顺便推荐基本Java的书籍，从左到由的顺序看到

Java：《Java核心技术卷1》、《编程思想》、《深入理解Java虚拟机》、《Java编程艺术》

数据库：《mysql必知必会》、《MySQL技术内幕：InnoDB存储引擎》

就先介绍这么多，这些都是最基础最核心滴，希望对那些不知道看什书的同学有所帮助
————————————————
版权声明：本文为CSDN博主「帅地」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/m0_37907797/article/details/102661778

书籍资源https://blog.csdn.net/JiuZhang_ninechapter/article/details/103670926?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task

英语https://language.chinadaily.com.cn/news_bilingual/
书籍https://wol.jw.org/cmn-Hans/wol/publication/r23/lp-chs/cl

internationalize \ ˌin-tər-ˈnash-nə-ˌlīz 注意发音 sh和n确实分开的，但是n和l直接链接发音，l承担了2个角色，并且应该省去了ə.

facebook成功的故事https://www.facebook.com/business/success

一本书读懂世界的第一本经济学书
By 梁小民 https://books.google.ca/books?id=ylC8DwAAQBAJ&pg=PT48&lpg=PT48&dq=%E4%B8%AD%E5%9B%BD%E6%98%AF%E5%88%B6%E5%BA%A6%E5%86%85%E7%BB%8F%E6%B5%8E++%E5%9B%BD%E5%A4%96%E6%98%AF%E6%8E%A2%E7%B4%A2%E7%A7%91%E5%AD%A6%E7%9A%84%E7%BB%8F%E6%B5%8E&source=bl&ots=NzAcBElbE1&sig=ACfU3U1Dzfzrfk4uIOidOFuYL_fKAwZHYg&hl=en&sa=X&ved=2ahUKEwi_-u_qj5HoAhWXr54KHTd_A3sQ6AEwAHoECAkQAQ#v=onepage&q=%E4%B8%AD%E5%9B%BD%E6%98%AF%E5%88%B6%E5%BA%A6%E5%86%85%E7%BB%8F%E6%B5%8E%20%20%E5%9B%BD%E5%A4%96%E6%98%AF%E6%8E%A2%E7%B4%A2%E7%A7%91%E5%AD%A6%E7%9A%84%E7%BB%8F%E6%B5%8E&f=false

medium 文章可以看了

新知识-- https://www.bbc.com/ukchina/simp/vert-cap-44319402
这是英文原文 --https://www.bbc.com/worklife/article/20180523-why-facebook-will-never-die
托马教授称之为"惊鸿一瞥"（glamourised glimpses）的心理效应

好的论文，免费的https://www.xzbu.com/

英语连读，来自豆瓣 https://www.douban.com/note/198230208/


我的盲区 -- https://www.todayusstock.com/


## 3.10
laparoscopy -- \ ˌla-pə-ˈrä-skə-pē --注意发音，和t几乎一样，前p发b，后p发p
the use of a long thin tube put into a cut made in the body in order to examine inside the body or do an operation:
Typically, patients would prefer laparoscopy to an open surgery.

typically -- \ ˈti-pi-k(ə-)lē p发b, k发k 注意发音， 这个发音很典型 p位于2位，k位于2以上，且前面的是t 有出气，所以k也出气，不浊化,而p主要是第二音节,所以看元音规则,不属于3 音节的看前面辅音规则

```
d: 
2音节
little  \ ˈli-tᵊl 
butter \ ˈbə-tər  
settle \ ˈse-tᵊl
mortal \ ˈmȯr-tᵊl
2音节以上
stability \ stə-ˈbi-lə-tē
optical -- \ ˈäp-ti-kəl

t:
2音节
gentle \ ˈjen-tᵊl 
mantle \ ˈman-tᵊl 
2音节以上
pivotal \ ˈpi-və-tᵊl
digital \ ˈdi-jə-tᵊl 
facility \ fə-ˈsi-lə-tē 
priority -- \ prī-ˈȯr-ə-tē 
majority \ mə-ˈjȯr-ə-tē 
```

constantly -- \ ˈkän(t)-stənt-lē
all the time or often: He's constantly changing his mind.

strive - \ ˈstrīv
to try hard to do sth, or make sth happen, esp. for a long time or agains difficulties.

ambient
existing or present around you
ambient sound

atmosphere --\ ˈat-mə-ˌsfir 注意发音 t完全浊化
the mixture of gases that surrounds some planets, such as the earth; the air 大气
the character or mood of a place or situation: the club provided a relaxed and friendly atmosphere for its members.


Noticeable -- \ ˈnō-tə-sə-bəl 完全符合t的规则，在前面，元音间，d
there's a noticeable improvement in your grades. : easy to see

influence
She was influenced by the common-sense views of her grandparents.
common-sense

present -- \ ˈpre-zᵊnt
a birthday present
did you wrap th present?

now: the present

to give, show, make known

to introduce a person:
I’m pleased to present my son, Charles.

to cause something:
Falling tax revenues present a problem for the city.

wrap --\ ˈrap
cover sth by putting sth such as paper or cloth round it.

## 3.9
something you give to someone or do for someone to express your feelings or intentions:
It isn’t a big present – it’s just a token of thanks for your help.
 

a feeling of liking someone or something:
[ U ] Pets should be treated with affection.
[ U ] Harriet felt great affection for him.
http://www.cxyym.com/2016/04/1561/
https://waimaoquan.alibaba.com/newbbs/topic/1547579
简单来说吧，外销眼中只有客户，而内销看到的是整个市场。 
https://tenor.com/ 国外表情
我加入的
#I Look Like A Surgeon

planet -- \ ˈpla-nət 注意发音 ə 是i
conservation \ ˌkän(t)-sər-ˈvā-shən ts连起来，注意发音

infrared \ ˌin-frə-ˈred 注意发音 frə很连贯，没有明显的ə
 science
describing light at the red end of the spectrum (= set of colors into which light is separated), which cannot be seen by human beings, and which gives out heat

inhabitant
a person or animal that lives in a particular place: 

发d :
little butter settle mortal after(弹舌) hospital(次重音在s) stability(看b)
发t: 重音 次重音 必发t
gentle mantle pivotal digital retail(有意思，可能是次重音缘故)
总结:能省则省，但是n后面没音了，为了保证继续能起头发t，太长的音节为了保证t有声，最后的也是t
t: 有n(用t打破n导致的非元声状态) ， 长的，重音
d: 前后元音(t和元音是相对存在)，短的，非重音 (stability长的本音出来t，但是重音是b所以还是出不来)
只有mn才其实拖出了气了，所以需要t(需要t重新拉起声音)，r不会,f也不会(after)...目前都不会
hospital因为重音在s，所以t算2音节，不算3音节长的
看元音，就是d, 
辅音有气的，s f +t t浊化，因为话这些音引导出浊化结束发音了，配合(2音节经典)
2音节以上看下面
辅音无气的 m n, t必须发生了，因为没音了，要t
2音节以上理论要t，看重音的音，清就保持t
浊就d, digital 或许是因为后面的l,或者g出气了
facility \ fə-ˈsi-lə-tē t
digital \ ˈdi-jə-tᵊl t
priority -- \ prī-ˈȯr-ə-tē --- t
majority \ mə-ˈjȯr-ə-tē t
stability \ stə-ˈbi-lə-tē d
optical -- \ ˈäp-ti-kəl 发d
看重音开始:
前面有清辅，或有r 这样的发声了，后面t不需要停下来.
前面没有有气的发声带出，也没有完全被 m, n 结束，"有音无气状态"， 需要浊化的d继续保持
不能光看音节，要看比如以下，p 是否参与了引导元音的状态，才决定有没有气
optical -- \ ˈäp-ti-kəl 
priority -- \ prī-ˈȯr-ə-tē

##  3.7

loose
I’d better sew that loose button before it comes off.  
come off 注意不同词典，解释不一，还有多变，自现其义
to happen as planned or to succeed
To move, or to move something downwards


stewardship \ ˈstü-ərd-ˌship 颠覆性发音sh发ch

nob
a round lump on the surface or end of something

[programming](https://hackr.io/)

[go](https://stackify.com/learn-go-tutorials/)

[go](https://www.tutorialspoint.com/computer_programming_tutorials.htm)

[learn](https://gitconnected.com/learn)

  

[学习go](https://learnku.com/go/t/24715)

[the go playground](https://play.golang.org/)

  

词典[APA Dictionary of Psychology](http://dictionary.apa.org)

http://www.memidex.com/

https://www.computer-dictionary-online.org/

http://www.learnersdictionary.com

http://webstersdictionary1828.com/Dictionary/

  

sss配置

```

https://www.google.com/search?q={searchTerms}&tbm=isch

https://www.google.com/search?q={searchTerms}

https://en.wikipedia.org/wiki/Special:Search?search={searchTerms}

https://translate.google.com/#en/pt/{searchTerms}

https://en.wiktionary.org/wiki/{searchTerms}

https://translate.google.com/#auto/zh-CN/{searchTerms}

https://zh.forvo.com/word/{searchTerms}/#en_usa

https://ahdictionary.com/word/search.html?q={searchTerms}

http://webstersdictionary1828.com/Dictionary/{searchTerms}

https://www.merriam-webster.com/dictionary/{searchTerms}

https://www.vocabulary.com/dictionary/{searchTerms}

https://dictionary.cambridge.org/us/dictionary/english/{searchTerms}

https://www.oxfordlearnersdictionaries.com/us/definition/american_english/{searchTerms}

https://www.lexico.com/en/definition/{searchTerms}

https://www.macmillandictionary.com/dictionary/british/{searchTerms}

https://www.collinsdictionary.com/dictionary/english/{searchTerms}

https://www.yourdictionary.com/{searchTerms}

https://www.dictionary.com/browse/{searchTerms}

https://www.powerthesaurus.org/{searchTerms}/synonyms

https://www.spellzone.com/dictionary/{searchTerms}

http://dict.cn/{searchTerms}

https://www.etymonline.com/word/{searchTerms}

https://www.google.com/search?q={searchTerms} site:{hostname}

```

## 3.6
[真正需要的](https://www.easypacelearning.com/english-books/english-books-for-download-pdf/category/20-common-useful-english-phrases)

https://www.quora.com/Where-can-I-find-a-list-of-the-10-000-most-important-English-words

https://www.talkenglish.com/vocabulary/english-vocabulary.aspx

https://www.wgtn.ac.nz/lals/about/staff/Publications/paul-nation/headwords-first-thousand.pdf

[好好学习句子](https://www.ihbristol.com/useful-english-expressions)

https://midobay.com/

http://www.espressoenglish.net/wp-content/uploads/free/500-Real-English-Phrases.pdf

https://www.englishspeak.com/en/english-phrases

字典https://enacademic.com/
https://www.macmillandictionary.com/dictionary/british 比US更好

evil 
the condition of being immoral, cruel, or bad, or an act of this type

assume   \ ə-ˈsüm
to accept something as true without question or proof: 

innocent 
(of a person) not guilty of a particular crime, or having no knowledge of the unpleasant and evil things in life, or (of words or an action) not intended to cause harm

moral \ ˈmȯr-əl 注意发音 Mr. ben理论不发ə
relating to standards of good behavior, honesty, and fair dealing, or showing high standards of this type: 

milestone \ ˈmī(-ə)l-ˌstōn 注意发音l o 非常经典的区别
a stone or post at the side of the road that shows the distance to various places, especially to the nearest large town


## 3.5
https://mp.weixin.qq.com/s/BatbfrYLbycsHE5Ksdwoow
4.t音的消失 当/t/位于/n/于元音之间时

Internet ’In（t）∂nз:t

https://zhuanlan.zhihu.com/p/109230363

https://zhuanlan.zhihu.com/p/89660011

美式发音中，当/t/和/p/在单词的中间，且后面的音属于非重读音节，则/t/浊化成/d/，/p/浊化成/b/。

例：butter /ˈbʌdər/，open/ˈəʊbən/

city/ˈsɪdi/，little/ˈlɪdl/

（美音中/t/音的浊化大大促进了英语流畅、放松的发音，/d/音是非常平滑的音，/t/音需要更多的体力，/d/发音时肌肉无需太紧张。美音中的/p/也可以浊化成/b/，但没有/t/的浊化常见。）

/t/和/d/的完全省略

1）当/t/和/d/音在两个辅音中间时，可以完全省略。

例：must do /t/音完全省略

2）/t/和/d/在词尾时，通常会失去爆破或省略。

（在交流中，单词是有语境的，不是独立存在的，因此省略尾音后，不会对交流造成影响。


4：/t/，/d/，/s/，/z/分别和/j/的连读

1）/t/+/j/=/tʃ/

例：can’t you do it /kæntʃu:/

what your name is /wɒtʃɔ:r/

2）/d/+/j/=/dʒ/

例：did you /dɪdʒu:/

find your /faɪndʒɔ:r/

（do you 也常常连读为/dʒu:/，连读时do中的o不发音）

3）/s/+/j/=/ʃ/

例：yes, you are /jeʃu:/

guess your age /ɡeʃɔ:r/

4）/z/+/j/=/ʒ/

例：how’s your family /haʊʒɔ:r/

she misses you /mɪsɪʒu:/

（you，your和 you’re 在实际发音时，很可能会轻读，you发/jə/，your发/jər/，you’re发/jər/。连读后具体的发音以实际情况为准。）

https://zhuanlan.zhihu.com/p/100868878

**一、连读**

**发音规则一：辅音+元音**

一句话中相邻的两个单词，前一个单词以辅音结尾，后一个单词以元音开始，拼读成“辅音+元音”。

**讲解：**你还记得汉语拼音中有些单词xi'an（西安）、ku'ai（酷爱）吗？如果去掉隔音符，就成了xian（先）、kuai（快）了。英文中几乎所有的句子都是从头拼到尾，简单地说：连音就是两个单词相遇能拼读就拼，不能拼读就让过。例如：Take~it~easy


**发音规则二：元音+元音**

一句话中相邻的两个单词，前一个单词以元音结尾，后一个单词以元音开始，则在两个元音之间加上一个轻微的 [j] 或 [w] 的音，拼读成“元音+ [j] 或 [w] +元音”。

**[i:]或[eɪ]结尾的元音+[j]+元音**

**以[u:]或 [əʊ] 结尾的元音+[w]+元音**

**发音规则三** **省略 [h] 的连续**

在连音规则中，以“h”开头的单词 [h] 音近乎省略。因为 [h] 发音很特殊——只是出气没有摩擦，所以拼读时好像被省略了。


**二、略读**

英文最明显的语音规则除了连读外，就是略读了。爆破音和爆破音相邻，第一个爆破音只形成阻碍，但不发生爆破，称为失爆；爆破音和其他辅音相邻，该爆破音不完全爆破。英语语音中的失爆和不完全爆破现象，我们简称为“略读”。略读是英语语音学习的重点，也是一个难点，掌握好略读，也就掌握了地道英语发音的制胜法宝！

**注意：**略读时并不是把整个音丢掉，而是发音时点到为止，有口型不发音或轻微发音。重要学术名词--爆破音：[p] [b] [t] [d] [k] [g]


**1、爆破音+爆破音=失去爆破**

**Tips：**  
六个爆破音中任意两个相遇，一个爆破音后紧跟着另一个爆破音时，前面一个音点到为止，形成阻碍，但不发生爆破；第二个音完全爆破；若第二个爆破音在词尾，则必须轻化。以一个爆破音结尾并以同一个爆破音开始时，只发一次音，前一个音只做好发音准备而不发音，直接发第二个音。

**2、爆破音[t]和[d]+鼻辅音[m]和[n]**

爆破音[t]和[d]后面紧跟鼻辅音[m]和[n]，[t]和[d]形成阻碍，在词末必须通过鼻腔爆破；发音时，舌尖紧贴上齿龈，稍放开立刻贴回，从爆破音到鼻音舌位不变，让气流通过鼻腔冲出，在词中则不完全爆破。



**3、爆破音[t]和[d]+舌边音[l]**

爆破音[t]和[d]后面紧跟舌边音[l]，则必须由舌两边爆破，这种情况多发生在词尾。爆破音爆破音[t]和[d]后面紧跟清晰舌边[l]，则为不完全爆破。

**4、爆破音+摩擦音/破擦音=失去爆破**

当爆破音后紧跟着摩擦音和破擦音时，该爆破音形成阻碍，但不完全爆破。  
摩擦音：[f][v][θ][ ð][s][ z][ ʃ][ ʒ ][h][r]

破擦音：[ts]-[dz],[tr]-[dr],[tʃ]-[dʒ]

intentional \ in-ˈtench-nəl 注意发音ch
ambiguous \ am-ˈbi-gyə-wəs 注意发音yə-w形成u
##  2020.3.3
[英语情景对话](https://www.learnrealeng.com/p/situational-dialogues.html)
https://eslgold.com/practice-speaking/conversation-phrases/low-beginner/

https://github.com/manwar/perlweeklychallenge-club

https://www.infoq.cn/article/7eYwX_3Ap7DRb5LedzUp

Javascript/HTML/CSS是很多人都会用到的，后面的是SQLSQL 是一门非常非常重要并且应该熟练掌握的语言(虽然它不能被称为程序语言)，我在这里用了两个非常，因为很多工程师有些过于轻视 SQL 了，并为此付出了惨重的代价。

　　如果你平时的编程工作涉及到业务功能，而不是纯粹的技术架构，一定会使用到数据库。SQL 就是数据的语言，通过它你可以和数据建立连接和沟通。如果你的数据访问模式写得很差，轻则代码性能一塌糊涂，重则引发 Bug，而涉及数据的问题，Bug 等级都比较高，后果可能很严重。

　　(关于 SQL，可以参考朱赟专栏文章“每个工程师都应该了解的：数据库知识”。)
python动态 
GO 语言 静态 暂时放弃
不考虑ruby
  Indeed.com上分析了25种编程_语言_
  
  

图标获取网站

https://favicongrabber.com/

https://faviconkit.com/

1. favicon \ ˈfa-və-ˌkän

1. a small icon associated with a particular website or page that is displayed in an Internet browser (as in the browser's address bar or in a list of favorites)

2. A favicon is a small symbol which helps users to recognize a website. Usually, it’s a simplified version of a logo or figurative mark, which is displayed next to the page title in a browser tab. For power users who use a lot of tabs at the same time or who attach tabs in their browser, the small square icon can sometimes be the only orientation aid between websites that are currently opened. As an example you can see the favicon of seobility.net here:

  

2. usual \ ˈyü-zhə-wəl

1. happening or done most of the time; ordinary

  
  

###  Multifunctional power tool

剑桥和朗文 mw vocabu wiki 最全

1. rehabilitate \ ˌrē-ə-ˈbi-lə-ˌtāt

1. to return someone to a healthy or usual condition or way of living, or to return something to good condition

  

2. chuck

1. a device for holding an object firmly in a machine

  

3. veterinary \ ˈve-tə-rə-ˌner-ē 注意发音t发d

  

4. medicine

1. a substance taken into the body in treating an illness

  

5. audiology \ ˌȯ-dē-ˈä-lə-jē

1. the area of science and medicine that is concerned with hearing and balance

  

6. laryngology \ ˌler-ən-ˈgä-lə-jē

1. The branch of physiology dealing with the larynx and its disorders

1. larynx \ ˈler-iŋ(k)s -- an organ in the throat which contains the vocal cords (= tissue that moves to produce the voice)

  

7. vocal \ ˈvō-kəl

1. relating to or produced by the voice, either in singing or speaking

  

8. intentionally

1. in a planned or intended way

  

9. intervention

1. the act or fact of becoming involved intentionally in a difficult situation

  

10. severe \ sə-ˈvir 注意发音ə还是ə，不是e

1. causing great pain, difficulty, damage, etc.; very serious

  

11. https://www.merriam-webster.com/dictionary/trauma 单词似乎有问题

1. trauma

-. severe shock caused by an injury

  

12. shock

1. a sudden, unexpected, and often unpleasant or offensive event, or the emotional or physical reaction to such an event

  

13.

  

##  power tools

1.

[ FB 高福翠 Галина Гао](https://www.facebook.com/profile.php?id=100025532490361&sk=photos&collection_token=100025532490361%3A2305272732%3A5&next_cursor=AQHR6E4IREiCIMr40S5fGpPuUhzy94v9mX9CzyMsFcYmjHVX0O0Y9brMOeZvFpp9JsdvX6r7kmG9NiftgoGWSC9TOg)

  

> [JIANGSU HEALTH MEDICAL TECHNOLOGY DEVELOPMENT CO., LTD.]

> [Harbin Health Medical Appliances Co.,Ltd]

> [Harbin Haiousi Business Co., Ltd.]

> [HealthHOS](www.cn-hos.com)

> [阿里主页](https://cn-hos.en.alibaba.com/)

>

> No. 68 Dongyuan Lane, Laozishan Town, Hongze District, 223001 Huaian City

  

2. [ZS ORTHO](https://www.zsortho.com/products/index.html)

1. HK 公司 Power Tools

  

##  topics

  

1. #rhinology #rhinologist #sinussurgery #skullbasesurgery #endoscopicsurgery #skullbase #surgery #ilooklikeasurgeon #womensurgeons #womeninsurgery #womeninmedicine #womeninotolaryngology #femalesurgeon #stanfordent #stanfordsurgery #stanforduniversity #stanfordhealthcare #stanfordhospital #education #teaching #doctor #wellness #health #sinus #sinusitis #sinusinfection

  

2. #‎skullbase‬ #earsurgery #neurosurgery #microsurgery #schwannoma #laryngology #entsurgery
3. 
##  2020.3.2
语法空格
https://www.oreilly.com/library/view/learning-perl-6/9781491977675/ch01.html

https://github.com/AlexDaniel/raku-golf-cheatsheet
https://news.ycombinator.com/news

https://www.evanmiller.org/a-review-of-perl-6.html

https://www.learningraku.com/

https://perlgeek.de/en/article/5-to-6

https://rakuadventcalendar.wordpress.com/

1. beginner \ bi-ˈgi-nər 注意发音

  

2. garage \ gə-ˈräzh 注意发音

1. a building where a car is kept, built next to or as part of a house

  

3. ritual \ ˈri-chə-wəl

1. a set of fixed actions and sometimes words performed regularly, especially as part of a ceremony.

  

4. advantage \ əd-ˈvan-tij 注意发音，a就是a不是ä

  

5. manipulate \ mə-ˈni-pyə-ˌlāt

1. control sth or someon to your advantage

  

6. theater \ ˈthē-ə-tər 注意发音t还是t

1. a building, room, or outside structure with rows of seats, each row usually higher than the one in front, from which people can watch a performance, a movie, or another activity.

  

7. dedication the willingness to give a lot of time and energy to something because it is important

  

8. possession \ pə-ˈze-shən

1. the fact that you have or own something.

  

9. resource \ ˈrē-ˌsȯrs

1. a useful or valuable possession or quality of a contry, organization, or person

  

10. comment \ ˈkä-ˌment 注意发音

  

11. embedded \ im-ˈbe-dəd 注意ə发音偏向i ，没有e，没有ə，说明的确是ə的嘴型弱读，

##  2.29

1. benefit \ ˈbe-nə-ˌfit 注意发音，和下面i类似，靠后的i有弱读现象，产生i和e之间的音

  

2. privilege \ ˈpriv-lij. 注意i ，前面的i明显，后面的接近i和e之间的音

1. an advantage that only one person or group of people has, usually because of their position or because they are rich 很明显的逻辑，有钱有势才行，特权

  

3. entry

1. the act of entering a place or joining a particular society or organization

  

4. entry-level

1. (of a product) basic and suitable for new users who may later move on to a more advanced product

  

They have a good range of entry-level computers for beginners.

  

​(of a job) at the lowest level in a company

is used to describe basic low-cost versions of products such as cars or computers that are suitable for people who have no previous experience or knowledge of them.

  

5. diagnose \ ˈdī-ig-ˌnōs 注意发音ig开始失去重音，到弱读

1. to recognize and name the exact character of a disease or a problem, by examining it

  

6. asterisk -- \ ˈa-stə-ˌrisk 注意发音 i 发ə

  

7. bracket --\ ˈbra-kət 注意发音ə发e

8. comma -- \ ˈkä-mə 对比下面的还有asterisk,

9. colon -- \ ˈkō-lən 发现，o的发音其实看后面字母，达到同一个目的

10. dollar -- \ ˈdä-lər

11. tile --\ ˈtil-də 根据多次经历，发舌头像上的欧 ō的音，不是o更不是优

12. parenthesis -- \ pə-ˈren(t)-thə-səs (t)-the发特tə的音

13. evaluate  \ i-ˈval-yə-ˌwāt -yü-ˌāt \第一次遇到读后面的yü-ˌāt ,注意发音
  

https://www.yourdictionary.com/entry-level 解释不错

[md参考](https://about.gitlab.com/handbook/engineering/ux/technical-writing/markdown-guide/#tips--tricks)

  

[md参考](https://learn.getgrav.org/16/content/markdown)
## md格式
网址里用-或者 %20 最好
网站多半是-或者空格

##2.28 
#  neurosurgery 词汇

格式记录33行

https://biologydictionary.net/

https://en.wiktionary.org/wiki/

  

https://www.lexico.com/en/definition/

https://www.medicinenet.com/medterms-medical-dictionary/article.htm

  

生僻的:

https://medical-dictionary.thefreedictionary.com/

https://www.merriam-webster.com/medical/

  

1. anatomy -- \ ə-ˈna-tə-mē

the scientific study of the body and how its parts are arranged

- scientific

- relating to science, or using the organized methods of science

2. transsphenoidal -- Through or across the sphenoid bone.

1. sphenoid - \ ˈsfē-ˌnȯid

- a bone in the lower part of the skull.

- butterfly-shaped bone at the base of the skull.

  

3. posture -- \ ˈpäs-chər

- posture is the position of a body while standing or sitting.

  

4. illustration -- \ ˌi-lə-ˈstrā-shən

- a picture in a book, magazine, etc. or the process of illustrating sth.

  

5. compliance -- \ kəm-ˈplī-ən(t)s

- the act of obeying an order, rule, or request.

  

6. inversion -- \ in-ˈvər-zhən 注意发音zh发 /ʒ/

  

7. personnel -- \ ˌpər-sə-ˈnel

1. the people who are employed in a company, organization, or one of the armed forces

- personnel vs employ

- 1: My boss said that he appreciated having me as his employee. 2: During the holiday season, there is a normal reduction in personnel in most companies.

  

8. optimal -- \ ˈäp-tə-məl

1. the best or most effective possible in a particular situation


## 2.28其他词汇
##  2.28

  

1. ratio -- \ ˈrā-(ˌ)shō

the retation ship between two groups or amounts that express how much bigger one is than the other.

  

2. probability --\ ˌprä-bə-ˈbi-lə-tē

the level of possibility of something happening or being true

  

3. odds \ ˈädz

the probability that a particular thing will or will not happen

  

- probability VS odds

- Odds are ratios between outcomes while a probability is the ratio between an outcome and all possible outcomes.

  

4. fairly --\ ˈfer-lē

more than average, but less than very

  

5. beam --\ ˈbēm 注意发音，明显的m

a line of light that shines from a bright object

  

6. radiation -- \ ˌrā-dē-ˈā-shən

a form of energy that comes from a nuclear reaction adn that can be very dangerous to health

  

7. nuclear -- \ ˈnü-klē-ər

being or using the power produced when the nucleus of an atom is divided or joined to another nucleus

8. nucleus -- \ ˈnü-klē-əs

PHYSICS: the central part of an atom, usually made up of protons and neutrons

BLOLOGY: the part of a cell that controls its arowth

  

9. atom --\ ˈa-təm t发弹舌音d

the smallest unit of any chemical element, consisting of a positive nucleus

  

10. property -- \ ˈprä-pər-tē p发b t 不变t

an object or objects that belong to someone

  

11. reputation --\ ˌre-pyə-ˈtā-shən 注意发音 p发b

12. general -- \ ˈjen-rəl 中间的e不发音，注意发音
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
eyJoaXN0b3J5IjpbLTkxMzc5NTc2OCwtOTM1NTY5NDIwLC02MD
M0MDU5MzgsMTE4NTM4NzI5NSwxMDU2MDgyNTc5LDE2NjE5OTc2
NjEsMTQxNDMwMzk3LC0yNjUzMjc2OTQsMTkyMzM1MDg1OSw5Mz
EwNjc1MTIsLTI2OTExMDIyNCwtMTE5NDc1MzM3NCwxMjEyMDc1
ODk4LDE0NTk0MjIxNzcsLTg0NjM3ODIzOCwyMDc2MzQ2NTQ0LC
0xNDQ1ODU5NjYzLC05OTEzMTEyNCwtMTUzNzI4NjAwMiwxNzY0
ODg5NjMzXX0=
-->