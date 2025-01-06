---
title: "ZSH - Tutorial notes (in Chinese)"
date: "2021-04-10"
tags: ["Terminal"]
---



# Zsh 配置

Zsh 的配置主要集中在用户当前目录的.zshrc里(在mac的用户目录下ls -a命令就可以看到)，用 vim 或你喜欢的其他编辑器打开.zshrc

```
	code .zshrc
	nano .zshrc
	vim .zshrc
```

可以在此处定义自己的环境变量和别名

```
	alias cls='clear'
	alias ll='ls -l'
	alias la='ls -a'
	alias vi='vim'
	alias javac="javac -J-Dfile.encoding=utf8"
	alias grep="grep --color=auto"
```

zsh 的霸气之处在于不仅设置通用别名，还能针对文件类型设置对应的打开程序

```
	alias -s html=mate   # 在命令行输入后缀html文件, 会在TextMate中打开
	alias -s rb=mate     # 在命令行直接输入ruby文件, 会在 TextMate 中打开
	alias -s py=vi       # 在命令行直接输入py  文件, 会用 vim 中打开
	alias -s js=vi
	alias -s c=vi
	alias -s java=vi
	alias -s txt=vi
	alias -s gz='tar -xzvf'
	alias -s tgz='tar -xzvf'
	alias -s zip='unzip'
	alias -s bz2='tar -xjvf'
```

(比如：`alias -s html=mate`，意思就是你在命令行输入 hello.html，zsh会为你自动打开 TextMat 并读取 hello.html； `alias -s gz='tar -xzvf'`，表示自动解压后缀为 gz 的压缩包)



# ZSH 快捷键

[https://www.zhihu.com/question/21418449](https://www.zhihu.com/question/21418449)
zsh 里面使用 bindkey 命令可以设置一系列热键，用来运行某一个 zsh 内部命令或者某个 shell 命令，谁规定终端只能敲字母呢？我们还可以按热键，比如从网上下载了一个 tar 包解开后要稍微浏览一下里面的内容，用的最多的两条命令是啥呢？第一条是 ls 命令，每到一个子目录都要先按一下，还有就是 cd .. 对吧，经过配置：

```bash
bindkey -s '\eo'   'cd ..\n'    # 按下ALT+O 就执行 cd .. 命令
bindkey -s '\e;'   'ls -l\n'    # 按下 ALT+; 就执行 ls -l 命令
```

你还可以设置一键打开编辑器，或者一键帮你输入某常用命令的一部分。除了这些命令外，日常命令编写也可以加强一下：

```bash
bindkey '\e[1;3D' backward-word       # ALT+左键：向后跳一个单词
bindkey '\e[1;3C' forward-word        # ALT+右键：前跳一个单词
bindkey '\e[1;3A' beginning-of-line   # ALT+上键：跳到行首
bindkey '\e[1;3B' end-of-line         # ALT+下键：调到行尾
```

敲命令时经常需要对已有命令进行修改，默认一个字符一个字符的跳太慢了，这样设置以后基于单词的跳转快速很多，配合其他一些快捷键，修改命令事半功倍。

终端下从 v220t 到 xterm 规范里，按下 alt+x 会先发送一个8位 ASCII 码 27，即 ESC键的扫描吗，然后跟着 x 这个字符，也等价于快速（比如100毫秒内）前后按下 ESC 和 x。

还不会再自己的终端软件里设置允许 alt 键的同学们可以搜索下相关文章。



# ZSH 功能

## 自动补全

基本命令/参数补全: 在输了一半的时候单击TAB可选择下一个补全选项, 多次单击可以顺序选择可选补全选项 (如果不使用插件, 则默认不展示选项)

![2023.11.23 - 210442](2023.11.23%20-%20210442.jpg)

补全目录: 在输了一半的时候连续快速敲击两次TAB即可进取补全选择界面, 可以通过上下左右选择补全选项, 也可以通过老的TAB选择 (在选择命令的参数, 参数较多的时候比较有用)

![2023.11.23 - 210451](2023.11.23%20-%20210451.jpg)

zsh-autosuggestions: 这个插件会在输入一般的时候在背景用低对比的字体显示出预测的输入, 预测会根据你的历史命令更新. 你可以跟着他的建议手动输入, 也可以直接按右方向键直接完成

![2023.11.23 - 210502](2023.11.23%20-%20210502.jpg)

## 快速跳转

输入 cd 后面加一个减号后，按一次 tab 马上就列出本次登陆后去过的最近几次路径，接着根据下面的提示输入数字按回车就过去了

![2023.11.23 - 210513](2023.11.23%20-%20210513.jpg)



## 历史记录搜索

zsh 的历史记录跨 session，可以共享。历史记录支持受限查找。比如，输入git，再按向上箭头，会搜索用过的所有 git 命令。

![2023.11.23 - 210531](2023.11.23%20-%20210531.jpg)



## 通配符搜索

打印所有文件

![2023.11.23 - 210543](2023.11.23%20-%20210543.jpg)

查找当前目录下文件

![2023.11.23 - 210634](2023.11.23%20-%20210634.jpg)

递归查找当前目录下的所有文件

![2023.11.23 - 210611](2023.11.23%20-%20210611.jpg)

