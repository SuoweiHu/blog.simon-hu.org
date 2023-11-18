---
title: ISO 8601 Time Encode
date: 2023-11-18
categories:
  - Learning
---

## Quick Reference Sheet

- Datetime - Basic Notation
	- `yyyymmddThhmmss
	- `20120915T155300`

- Datetime - Extended Notation 
	- Date and time in UTC
		- `2023-11-17T23:17:30Z`
	- Date and time with the offset
		- `yyyy-mm-ddT hh:mm:ss+|– hhmm`
		- `2012-09-15T15:53:00+04:30` (UTC+04:30)
		- `2023-11-17T16:17:30−07:00` (UTC−07:00)
		- `2023-11-17T23:17:30+00:00` (UTC+00:00)
		- `2023-11-18T06:17:30+07:00` (UTC+07:00)

## BTT Configuration 

- `(BTT)@dateformat:yyyy-MM-dd(BTT)`
- `(BTT)@dateformat:yyyy-MM-dd'T'HHmmss'AEST'(BTT)`


---
## Reference 
- [\*(BEST) Understanding ISO8610 Datetime Format](https://forum.obsidian.md/t/horizontal-rule-sometimes-changes-text-size-offers-folding-etc/7047)
- [Wikipedia - ISO 8610](https://en.wikipedia.org/wiki/ISO_8601)
- [Standard date and time format strings](https://learn.microsoft.com/en-us/dotnet/standard/base-types/standard-date-and-time-format-strings)
- [Date & time formats cheatsheet](https://devhints.io/datetime)
- [UNIX - strftime format cheatsheet](https://devhints.io/strftime)