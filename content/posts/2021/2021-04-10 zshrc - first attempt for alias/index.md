---
title: "ZSH - First attempt for alias in zshrc"
date: 2021-04-10
tags: ["zsh"]
---

```
# ========================================================= DIRECTORY =========================================================
# NOTE:
# - DO NOT comment any of the one line, as the posterior commands might be based on them
setopt INTERACTIVE_COMMENTS                         # Enable comment feature for the ZSH (with hash \#)
alias cls='clear'                                   # Use CLS rather than clear (being consistent with WIN)
export ROOT="/"
# export HOME="~"
export DESKTOP="/Users/suoweihu/Desktop"
export DOWNLOAD="/Users/suoweihu/Downloads"
export DOWNLOADS="/Users/suoweihu/Downloads"
#
# ===============================================================================================================================


# ========================================================= DIRECTORY =========================================================
# NOTE:
# - lsd has been delted for the simplicity's sake
# -
#
# LS
alias ll='ls -l'                                    # Use ll for ls -l (print in files in list formatte)
alias la='ls -a'                                    # Use la for ls -a (print all files)
#
# CD
alias cddesktop='cd /Users/suoweihu/Desktop'        # open desktop folder
alias cddownload='cd /Users/suoweihu/Downloads'     # open download folder
alias cddownloads='cd /Users/suoweihu/Downloads'    # open download folder (s)
alias cdroot='cd /'                                 # open root folder
alias cdhome='cd ~'                                 # open user's home folder
#
# PWD
alias showpath='pwd'                                # show current path
alias copypath='pwd|pbcopy'                         # copy current path
#
# ===============================================================================================================================


# ============================================================ PROMPT ============================================================
# NOTE:
# - This is for changing the prompt on the left of the screen, please use ONE-LINE ONLY
# - (e.g from "suoweihu@SH-MacBook Downloads % " to "Downloads > ")
# - If you wish to revert the initial setting, use "export PS1="%n@%m %1~ %# "
#
# export PS1="%n@%m %1~ %# "                        # Original PS1 file      (e.g suoweihu@SH-MacBook Downloads %)
export PS1="%1~ > "                                 # Show the last 1 element in the file path (e.g ~/Downloads >)
# export PS1="%2~ > "                               # Show the last 2 element in the file path (e.g   Downloads >)
# export PS1="%~ > "                                # Show the full path         (e.g /Users/suoweihu/Downloads >)
#
# ===============================================================================================================================


# ========================================================= YouTube -DL =========================================================
# NOTE:
# - The commented one may not work for the maintainance sake
# - Try to avoid using the more complex command as they use dependencides such as FFMPEG (bestAudio + bestVideo)
#
# GenericUsage
alias dl='downloadToDownloadFolder() { youtube-dl -o "~/Downloads/YouTube-dl/%(title)s-%(id)s.%(ext)s" $1 }; downloadToDownloadFolder'                     # Generic Download  (Normal quality video to Downlaod Folder)
# alias dlto='downloadToDownloadFolder() { youtube-dl -o "~/Downloads/YouTube-dl/%(title)s-%(id).%(ext)s" $1 }; downloadToDownloadFolder'                 # Generic Download  (Normal quality video to Downlaod Folder)
# alias dl='downloadVideo() { youtube-dl -f  $1 }; downloadVideo'                                                                                   # Generic Download  (Normal quality video to current Folder)
#
# Intermediate
# alias dlas='downloadAsFileName() { youtube-dl -o "~/Downloads/YouTube-dl/$2" $1 }; downloadAsFileName'    # Download with specified file name
alias dlvideo='downloadBestVideo() { youtube-dl -f bestvideo+bestaudio $1 }; downloadBestVideo'             # Download best quality video and audio and merge
# alias dlaudio='downloadAudio() { youtube-dl -x $1 }; downloadAudio'                                       # Download audio (By default it is OGG format)
alias dlaudio='downloadAudio() { youtube-dl -x --audio-format mp3 $1 }; downloadAudio'                      # Download audio (To mp3 format)
# alias dlplaylist='downloadPlaylist() { youtube-dl -i -f mp4 --yes-playlist $1 }; downloadPlaylist'        # Download play list
#
# Complex Commands
alias dlwithinfo='downloadWithInfo(){youtube-dl --write-description --write-info-json --write-annotations --write-sub --write-thumbnail $1}; downloadWithInfo'                                          # Download with decrption, meta data, annotation, subtitle and  
alias dlplaylist='dlPlaylistToDLFolder() { youtube-dl -o "~/Downloads/YouTube-dl/%(playlist_title)s/%(playlist_index)s-%(title)s-%(id)s.%(ext)s" $1 }; dlPlaylistToDLFolder'                                   # Download Playlist (Normal quality video to Downlaod Folder) with labelling of video's index
alias dlaudioplaylist='dlPlaylistToDLFolder() { youtube-dl -i -x --audio-format mp3 -o "~/Downloads/YouTube-dl/%(playlist_title)s/%(playlist_index)s-%(title)s-%(id)s.%(ext)s" $1 }; dlPlaylistToDLFolder'        # Download Playlist (Normal quality video to Downlaod Folder) with labelling of video's index

#
# ===============================================================================================================================


autoload -U compinit                                # auto complete (deletable)
compinit                                            # auto complete (deletable)
# alias example='f() { echo Your arg was $1. };f'   # Example of making a function in ZSH
```
