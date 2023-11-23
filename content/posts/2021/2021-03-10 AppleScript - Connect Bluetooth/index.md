---
title: "AppleScript - Connect Bluetooth"
date: "2021-03-10"
tags: ["AppleScript"]
categories: ["Utility"]
---

```
tell application "System Events" to tell process "SystemUIServer"
	set bt to (first menu bar item whose description is "bluetooth") of menu bar 1
	click bt
	tell (first menu item whose title is "SH-Airpods") of menu of bt
		click
		tell menu 1
			if exists menu item "Connect" then
				click menu item "Connect"
			else
				if exists menu item "Disconnect" then
					click menu item "Disonnect"
				else
					if exists menu item "连接" then
						click menu item "连接"
					else
						if exists menu item "断开连接" then
							click menu item "断开连接"
						else
							click bt
						end if
					end if
				end if
			end if
		end tell
	end tell
end tell
```