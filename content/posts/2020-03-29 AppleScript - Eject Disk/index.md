---
title: "AppleScript - Eject Disk"
date: "2020-03-29"
tags: ["AppleScript"]
categories: ["Utility"]
---

## Simple Versiom
```applescript
set diskName to "YourDiskNameHere"
tell application "Finder"
	if disk diskName exists then
		eject disk diskName
	end if
end tell
```

## More Complex Version
(If disk is currently mounted then unmount, otherwise reverse the process )

```applescript
set diskName to "YourDiskNameHere"
tell application "Finder"
 if disk diskName exists then
  eject disk diskName
 else
  tell current application
   set deviceLine to (do shell script "diskutil list | grep \"" & diskName & "\" | awk '{ print $NF }' }'")
   if deviceLine = "" then
    display dialog "The disk \"" & diskName & "\" cannot be found." buttons {"OK"} default button 1 with title "Error" with icon caution
   end if
   set foundDisks to paragraphs of deviceLine
   repeat with i from 1 to number of items in foundDisks
    set this_item to item i of foundDisks
    if this_item contains "disk" then
     do shell script "diskutil mountDisk /dev/" & this_item
    end if
   end repeat
  end tell
 end if
end tell
```

## Usage Example
```applescript
set diskName to "Physical-1號"
tell application "Finder"
	if disk diskName exists then
		eject disk diskName
	end if
end tell
set diskName to "Physical-2號"
tell application "Finder"
	if disk diskName exists then
		eject disk diskName
	end if
end tell
set diskName to "Physical-3號"
tell application "Finder"
	if disk diskName exists then
		eject disk diskName
	end if
end tell
set diskName to "Physical-4號"
tell application "Finder"
	if disk diskName exists then
		eject disk diskName
	end if
end tell
set diskName to "Physical-5號"
tell application "Finder"
	if disk diskName exists then
		eject disk diskName
	end if
end tell
set diskName to "Physical-6號"
tell application "Finder"
	if disk diskName exists then
		eject disk diskName
	end if
end tell

```


## Reference

[http://hints.macworld.com/article.php?story=20120211184732735](http://hints.macworld.com/article.php?story=20120211184732735)
