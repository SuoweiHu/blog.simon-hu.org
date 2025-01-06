---
title: "AppleScript - Insert Datetime (of format)"
date: "2021-03-07"
tags: ["AppleScript", "Utility"]
---




## Dot Delininated Format Date
Input
```applescript
on zero_pad(value, string_length)
	set string_zeroes to ""
	set digits_to_pad to string_length - (length of (value as string))
	if digits_to_pad > 0 then
		repeat digits_to_pad times
			set string_zeroes to string_zeroes & "0" as string
		end repeat
	end if
	set padded_value to string_zeroes & value as string
	return padded_value
end zero_pad

on run
	set now to (current date)

	set result to (year of now as integer) as string
	set result to result & "."
	set result to result & zero_pad(month of now as integer, 2)
	set result to result & "."
	set result to result & zero_pad(day of now as integer, 2)
	set the clipboard to the result
end run
```
Output
```
2021.03.07
```


## Complete Date - default datetime format
Input
```applescript
set date_ to ((current date) as string)
set the clipboard to the date_
```
Output
```
Sunday, 7 March 2021 at 2:01:15 pm
```



## Complete date - bar deliminated format
Input
```applescript
on zero_pad(value, string_length)
	set string_zeroes to ""
	set digits_to_pad to string_length - (length of (value as string))
	if digits_to_pad > 0 then
		repeat digits_to_pad times
			set string_zeroes to string_zeroes & "0" as string
		end repeat
	end if
	set padded_value to string_zeroes & value as string
	return padded_value
end zero_pad

on run
	set now to (current date)

	set result to (year of now as integer) as string
	set result to result & "-"
	set result to result & zero_pad(month of now as integer, 2)
	set result to result & "-"
	set result to result & zero_pad(day of now as integer, 2)
	set result to result & " "
	set result to result & zero_pad(hours of now as integer, 2)
	set result to result & ":"
	set result to result & zero_pad(minutes of now as integer, 2)
	set result to result & ":"
	set result to result & zero_pad(seconds of now as integer, 2)

	return result
end run
```
Output
```
2021-03-07 14:25:17
```

