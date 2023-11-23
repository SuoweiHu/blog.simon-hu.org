---
title: "ZSH - Trojan Proxy & Shell Prompt (PS1)"
date: 2021-04-14
categories: ["zsh"]
---

```
# If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:/usr/local/bin:$PATH

# Path to your oh-my-zsh installation.          ( 关闭此选项以关闭使用 oh-my-zsh )
export ZSH="/Users/suoweihu/.oh-my-zsh"

# Set name of the theme to load --- if set to "random", it will
# load a random theme each time oh-my-zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
# ZSH_THEME="robbyrussell"                 ( ZSH 主题 ls .oh-my-zsh/themes 查看所有主题 )
# ZSH_THEME="wedisagree"
ZSH_THTEME="cloud"

# Set list of themes to pick from when loading at random
# Setting this variable when ZSH_THEME=random will cause zsh to load
# a theme from this variable instead of looking in $ZSH/themes/
# If set to an empty array, this variable will have no effect.
# ZSH_THEME_RANDOM_CANDIDATES=( "robbyrussell" "agnoster" )

# Uncomment the following line to use case-sensitive completion.
# CASE_SENSITIVE="true"

# Uncomment the following line to use hyphen-insensitive completion.
# Case-sensitive completion must be off. _ and - will be interchangeable.
# HYPHEN_INSENSITIVE="true"

# Uncomment the following line to disable bi-weekly auto-update checks.
# DISABLE_AUTO_UPDATE="true"

# Uncomment the following line to automatically update without prompting.
# DISABLE_UPDATE_PROMPT="true"

# Uncomment the following line to change how often to auto-update (in days).
# export UPDATE_ZSH_DAYS=13

# Uncomment the following line if pasting URLs and other text is messed up.
# DISABLE_MAGIC_FUNCTIONS="true"

# Uncomment the following line to disable colors in ls.
# DISABLE_LS_COLORS="true"

# Uncomment the following line to disable auto-setting terminal title.
# DISABLE_AUTO_TITLE="true"

# Uncomment the following line to enable command auto-correction.
# ENABLE_CORRECTION="true"

# Uncomment the following line to display red dots whilst waiting for completion.
# COMPLETION_WAITING_DOTS="true"

# Uncomment the following line if you want to disable marking untracked files
# under VCS as dirty. This makes repository status check for large repositories
# much, much faster.
# DISABLE_UNTRACKED_FILES_DIRTY="true"

# Uncomment the following line if you want to change the command execution time
# stamp shown in the history command output.
# You can set one of the optional three formats:
# "mm/dd/yyyy"|"dd.mm.yyyy"|"yyyy-mm-dd"
# or set a custom format using the strftime function format specifications,
# see 'man strftime' for details.
# HIST_STAMPS="mm/dd/yyyy"

# Would you like to use another custom folder than $ZSH/custom?
# ZSH_CUSTOM=/path/to/new-custom-folder

# Which plugins would you like to load?
# Standard plugins can be found in $ZSH/plugins/
# Custom plugins may be added to $ZSH_CUSTOM/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(
    git                 # Github
    zsh-autosuggestions # https://github.com/zsh-users/zsh-autosuggestions
)

source $ZSH/oh-my-zsh.sh
source ~/.oh-my-zsh/plugins/incr/incr*.zsh

# User configuration

# export MANPATH="/usr/local/man:$MANPATH"

# You may need to manually set your language environment
# export LANG=en_US.UTF-8

# Preferred editor for local and remote sessions
# if [[ -n $SSH_CONNECTION ]]; then
#   export EDITOR='vim'
# else
#   export EDITOR='mvim'
# fi

# Compilation flags
# export ARCHFLAGS="-arch x86_64"

# Set personal aliases, overriding those provided by oh-my-zsh libs,
# plugins, and themes. Aliases can be placed here, though oh-my-zsh
# users are encouraged to define aliases within the ZSH_CUSTOM folder.
# For a full list of active aliases, run `alias`.
#
# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"







# =================================================================================================================
# =================================================================================================================
#
# /‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾\
# |    Alias Tutorial     |
# \_______________________/
#
# - Simple Alias:       (简单化名)
#
#                       ``` alias _DESKTOP_='/Users/suoweihu/Desktop' ````
#                       在命令行输入 '_DESKTOP_' 字段的时候, 会被'/Users/suoweihu/Desktop' 替换 (${_DESKTOP_})
#                       (echo ${_DESKTOP_} --> echo '/Users/suoweihu/Desktop')
#                       (cd _DESKTOP       --> cd '/Users/suoweihu/Desktop')
#
#                       ``` alias ip="curl cip.cc" ```
#                       在命令行输入 'ip' 字段的时候, 会执行'curl cip.cc'
#                       (ip                --> curl cip.cc)
#
#
# - Suffix Alias:       (后缀化名)
#
#                       ``` alias -s zip='unzip' ```
#                        在命令行输入 zip 后缀文件, 会使用unzip打开
#                       ('file_name.zip'         --> 'unzip file_name.zip')
#
#                       ``` alias -s suffix_name='command -option' ```
#                       在命令行输入后缀为 suffix_name 的文件, 会使用command -option打开
#                       ('file_name.suffix_name' --> 'command -option file_name.suffix_name')
#
#                       ```alias -s {cs,ts,html}=code```
#                       在命令行输入后缀为 cs,ts,html 的文件, 会使用code打开
#                       ('file_name.cs/ts/html'  --> 'code file_name.cs/ts/html')
#
#
# - Function Alias:     (函数化名)
#
#                       ``` alias_name(){
#                           command_a $firstParam $secondParam
#                           command_b $thirdParam $forthParam
#                       } ```
#                       在命令行输入 alias_name(1,2,3,4) 的时候会运行 'command_a 1 2 && command_b 3 4'
#
#                       (alias_name(1,2,3,4) --> command_a 1 2 && command_b 3 4)
#                       ```getaks() {
#                             az aks list -g $1 -o $2
#                       }```
#                       (getaks resource-group-1 jsonc --> az aks list -g esource-group-1 -o jsonc)
#
#
# - Global Alias:       (全局化名) 简述
#
#                       ``` alias -g qId="--query id -o tsv" ````
#                       全局化名会替代激进的所有的已有化名
#                       (USAGE: az aks show -n myaks2020 -g rg-demo --query id -o tsv)
#
#
# - OperSys Spec:       (针对操作系统的化名) 简述
#
#                       ```
#                       # macOS aliasses
#                       if [[ $OSTYPE == darwin* ]]; then
#                       alias flush='dscacheutil -flushcache'
#                       # Apps
#                       alias browse="open -a /Applications/Google\ Chrome.app"
#                       # * Browse Azure Portal
#                       alias azure="browse https://preview.portal.azure.com"
#                       fi
#                       ```
# =================================================================================================================
# =================================================================================================================





# /‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾\
# |      File Suffix      |
# \_______________________/

# alias javac="javac -J-Dfile.encoding=utf8"
# alias grep="grep --color=auto"
# alias -s html=mate   # 在命令行直接输入后缀为 html 的文件名，会在 TextMate 中打开
# alias -s rb=mate     # 在命令行直接输入 ruby 文件，会在 TextMate 中打开
# alias -s py=vi       # 在命令行直接输入 python 文件，会用 vim 中打开，以下类似
# alias -s js=vi
# alias -s c=vi
# alias -s java=vi
# alias -s txt=vi
# alias -s gz='tar -xzvf'
# alias -s tgz='tar -xzvf'
# alias -s zip='unzip'
# alias -s bz2='tar -xjvf'


# /‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾\
# |    Must Have Alias    |
# \_______________________/


# NOTE:
# - DO NOT comment any of the one line, as the posterior commands might be based on them

# ZSH 设置
# export ZSH="/Users/suoweihu/.oh-my-zsh"
# export ZSH="/Users/suoweihu/.zshrc"
# source $ZSH/oh-my-zsh.sh


# 环境变量配置 (Environmental1 Variable)
export ROOT="/"
export HOME="/Users/suoweihu"
export DESKTOP="/Users/suoweihu/Desktop"
export DOWNLOAD="/Users/suoweihu/Downloads"
export DOWNLOADS="/Users/suoweihu/Downloads"
# export PATH=$PATH:/Users/suoweihu/opt/GNAT/2019/bin  # For ada compilation of gnatmake 2019
# export PATH=$PATH:/Users/suoweihu/opt/GNAT/2018/bin  # For ada compilation of gnatmake 2018
# PATH="/Library/Frameworks/Python.framework/Versions/3.9/bin:${PATH}" # For pyton 2.7 to 3.9
# export PATH

setopt INTERACTIVE_COMMENTS                         # Enable comment feature for the ZSH (with hash \#)
autoload -U compinit                                # auto complete (deletable)
compinit                                            # auto complete (deletable)
# alias example='f() { echo Your arg was $1. };f'   # Example of making a function in ZSH
alias cls='clear'                                   # Use CLS rather than clear (being consistent with WIN)









# /‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾\
# |   ZSH Prompt Style    |
# \_______________________/

# NOTE:
# - This is for changing the prompt on the left of the screen, please use ONE-LINE ONLY
# - (e.g from "suoweihu@SH-MacBook Downloads % " to "Downloads > ")
# - If you wish to revert the initial setting, use "export PS1="%n@%m %1~ %# "
#
# export PS1="%n@%m %1~ %# "                        # Original PS1 file      (e.g suoweihu@SH-MacBook Downloads %)
# export PS1="%1~ > "                               # Show the last 1 element in the file path (e.g ~/Downloads >)
# export PS1="%2~ > "                               # Show the last 2 element in the file path (e.g   Downloads >)
# export PS1="%~ > "                                # Show the full path         (e.g /Users/suoweihu/Downloads >)
#
# export PS1="[%1~] "                               # Curretnly Using
#
#
# alias ec="$EDITOR $HOME/.zshrc"                   # (修改.zshrc文件) open ~/.zshrc in using the default editor specified in $EDITOR
# alias sc="source $HOME/.zshrc"                    # (更新.zshrc配置) source ~/.zshrc
alias edit_zshrc="code $HOME/.zshrc"                # (修改.zshrc文件)
alias reload_zshrc="source $HOME/.zshrc"            # (更新.zshrc配置)
alias update_zshrc="edit_zshrc;"                    # (更新.zshrc配置)
alias zshrc_edit="edit_zshrc;"                      # (修改.zshrc文件)
alias zshrc_reload="reload_zshrc;"                  # (更新.zshrc配置)
#
alias my_shell="echo $SHELL"                        # 查看我的SHELL










# /‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾\
# |      Navigation       |
# \_______________________/

# Note:
# - lsd has been delted for the simplicity's sake

# LS
alias ll='ls -l'                                    # Use ll for ls -l (print in files in list formatte)
alias la='ls -a'                                    # Use la for ls -a (print all files)
# CD
alias cddesktop='cd /Users/suoweihu/Desktop'        # open desktop folder
alias cddownload='cd /Users/suoweihu/Downloads'     # open download folder
alias cddownloads='cd /Users/suoweihu/Downloads'    # open download folder (s)
alias cdroot='cd /'                                 # open root folder
alias cdhome='cd ~'                                 # open user's home folder
# PWD
alias showpath='pwd'                                # show current path
alias copypath='pwd|pbcopy'                         # copy current path











# /‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾\
# |      YouTube DL       |
# \_______________________/

# NOTE:
# - The commented one may not work for the maintainance sake
# - Try to avoid using the more complex command as they use dependencides such as FFMPEG (bestAudio + bestVideo)

# GenericUsage (普通使用)
alias dl='downloadToDownloadFolder() { youtube-dl -o "~/Downloads/YouTube-dl/%(title)s-%(id)s.%(ext)s" $1 }; downloadToDownloadFolder'                     # Generic Download  (Normal quality video to Downlaod Folder)
alias ydl='downloadToDownloadFolder() { youtube-dl -o "~/Downloads/YouTube-dl/%(title)s-%(id)s.%(ext)s" $1 }; downloadToDownloadFolder'                    # Generic Download  (Normal quality video to Downlaod Folder)
alias youtubedl='downloadToDownloadFolder() { youtube-dl -o "~/Downloads/YouTube-dl/%(title)s-%(id)s.%(ext)s" $1 }; downloadToDownloadFolder'              # Generic Download  (Normal quality video to Downlaod Folder)
# alias dlto='downloadToDownloadFolder() { youtube-dl -o "~/Downloads/YouTube-dl/%(title)s-%(id).%(ext)s" $1 }; downloadToDownloadFolder'                 # Generic Download  (Normal quality video to Downlaod Folder)
# alias dl='downloadVideo() { youtube-dl -f  $1 }; downloadVideo'                                                                                   # Generic Download  (Normal quality video to current Folder)
#
# Intermediate (最佳画质/音质)
# alias dlas='downloadAsFileName() { youtube-dl -o "~/Downloads/YouTube-dl/$2" $1 }; downloadAsFileName'    # Download with specified file name
alias dlvideo='downloadBestVideo() { youtube-dl -f bestvideo+bestaudio $1 }; downloadBestVideo'             # Download best quality video and audio and merge
# alias dlaudio='downloadAudio() { youtube-dl -x $1 }; downloadAudio'                                       # Download audio (By default it is OGG format)
alias dlaudio='downloadAudio() { youtube-dl -x --audio-format mp3 $1 }; downloadAudio'                      # Download audio (To mp3 format)
# alias dlplaylist='downloadPlaylist() { youtube-dl -i -f mp4 --yes-playlist $1 }; downloadPlaylist'        # Download play list
#
# Complex Commands (复杂命令)
alias dlwithinfo='downloadWithInfo(){youtube-dl --write-description --write-info-json --write-annotations --write-sub --write-thumbnail $1}; downloadWithInfo'                                                    # Download with decrption, meta data, annotation, subtitle and  
alias dlplaylist='dlPlaylistToDLFolder() { youtube-dl -o "~/Downloads/YouTube-dl/%(playlist_title)s/%(playlist_index)s-%(title)s-%(id)s.%(ext)s" $1 }; dlPlaylistToDLFolder'                                      # Download Playlist (Normal quality video to Downlaod Folder) with labelling of video's index
alias dlaudioplaylist='dlPlaylistToDLFolder() { youtube-dl -i -x --audio-format mp3 -o "~/Downloads/YouTube-dl/%(playlist_title)s/%(playlist_index)s-%(title)s-%(id)s.%(ext)s" $1 }; dlPlaylistToDLFolder'        # Download Playlist (Normal quality video to Downlaod Folder) with labelling of video's index







# /‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾\
# |        Proxy          |
# \_______________________/

# IP : 查询公网地址
alias ip="curl cip.cc"              # (多行) IP	: 172.104.86.42 \n 地址	: 日本  东京都  品川区 \n 运营商	: linode.com \n 数据二	: 日本 | 东京Linode数据中心 \n 数据三	:  \n URL	: http://www.cip.cc/172.104.86.42
# alias ip="curl ipinfo.io"         # (多行) { "ip": "114.110.1.38", "hostname": "No Hostname", "city": "Beijing", "region": "Beijing Shi", "country": "CN", "loc": "39.9289,116.3883", "org": "AS4808 CNCGROUP IP network China169 Beijing Province Network"}%
# alias ip="curl https://ip.cn"     # (单行) 当前 IP: 120.133.6.22 来自: 天津市 第一线
# alias ip="curl myip.ipip.net"     # (单行) 当前 IP：114.110.1.38  来自于：中国 北京 北京 联通/电信

# V2Ray
# export https_proxy="http://127.0.0.1:8001"; export HTTPS_PROXY="http://127.0.0.1:8001"
# export http_proxy="http://127.0.0.1:48738"; export https_proxy="http://127.0.0.1:48738";
# alias setproxy="export ALL_PROXY=http://127.0.0.1:48738"
# alias unsetproxy="unset ALL_PROXY"

# Trojan
alias useProxy_http="export HTTP_PROXY=http://127.0.0.1:58591;"
alias useProxy_https="export HTTPS_PROXY=http://127.0.0.1:58591;"
alias useProxy_all="export ALL_PROXY=socks5://127.0.0.1:51837;"
alias unsetProxy_http="unset HTTP_PROXY"
alias unsetProxy_https="unset HTTPS_PROXY"
alias unsetProxy_all="unset ALL_PROXY"
proxy_on(){
    # 设置转发
    useProxy_http;      # export HTTP_PROXY=http://127.0.0.1:58591;
    useProxy_https;     # export HTTPS_PROXY=http://127.0.0.1:58591;
    useProxy_all;       # export ALL_PROXY=socks5://127.0.0.1:51837;

    # 打印信息
    clear;
    echo "";
    # echo "/‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾\\";
    # echo "|  The terminal traffic has been proxied  |";
    # echo "\\_________________________________________/";
    echo "                ____________               "
    echo "---------------| Proxy :On  |--------------"
    echo "                ‾‾‾‾‾‾‾‾‾‾‾‾               "
    echo ""
    ip;                 # Print new IP info
    echo ""
    echo "         ___________________________       "
    echo "--------| Press any key to exit ... |------"
    echo "         ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾       "
    read user_random_input;
    clear;
}
proxy_off(){
    # 取消转发
    unsetProxy_http;      # export HTTP_PROXY=http://127.0.0.1:58591;
    unsetProxy_https;     # export HTTPS_PROXY=http://127.0.0.1:58591;
    unsetProxy_all;       # export ALL_PROXY=socks5://127.0.0.1:51837;

    # 打印信息
    clear;
    echo "";
    # echo "/‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾\\";
    # echo "|  The terminal traffic has been proxied  |";
    # echo "\\_________________________________________/";
    echo "                ____________               "
    echo "---------------| Proxy :Off |--------------"
    echo "                ‾‾‾‾‾‾‾‾‾‾‾‾               "
    echo ""
    ip;                 # Print new IP info
    echo ""
    echo "         ___________________________       "
    echo "--------| Press any key to exit ... |------"
    echo "         ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾       "
    read user_random_input;
    clear;
}





# /‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾\
# |  Brew Update/Upgrade  |
# \_______________________/

# Unshallow
# git -C /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core fetch --unshallow
# git -C /usr/local/Homebrew/Library/Taps/homebrew/homebrew-cask fetch --unshallow

# 开启下面的选项, 以自动执行更新命令
# brew update       # UPDATE: update is used to download package information from all configured sources.
                    # (从源服务器下载的metadata, 包括这个源有什么包, 包是什么版本, 下一个新的版本去哪里下等等)
# brew outdated     # 查看过时的包
# brew upgrade      # 通过源服务器通过update命令下载的metadata, 更新所有的包
# brew cleanup      # 删除过时的包, 包括作为依赖被下下来但是不再被需要的
                    # (Homebrew不会帮我们自动移除旧版本的软件包,你需要手动执行该命令去移除软件包)

# Update,Upgrade (更新/升级)
alias bubo='brew update && brew outdated'
alias bubc='brew upgrade && brew cleanup'
alias bubu='bubo && bubc'


alias python="/Library/Frameworks/Python.framework/Versions/3.9/bin/python3"
alias python="/Library/Frameworks/Python.framework/Versions/3.9/bin/python3.9"
```