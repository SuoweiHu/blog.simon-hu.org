---
title: "Awk command 101"
date: "2024-06-04"
categories: ["CLI", "Linux"]
---



## Overview

### What is AWK command ?

>   The basic function of `awk` is to **<u>search files for lines (or other units of text) that contain certain patterns</u>**. When a line **<u>matches</u>** one of the patterns, `awk` **<u>performs specified action</u>**s on that line. `awk` continues to process input lines in this way until it reaches the end of the input files.
>
>   -- [GNU General Instruction for AWK](https://www.gnu.org/software/gawk/manual/gawk.html#Getting-Started)

### What does it specialises in ?

>   Programs in `awk` are different from programs in most other languages, because `awk` programs are **<u>*data driven*</u>** (i.e., you describe the data you want to work with and then what to do when you find it). Most other languages are ***<u>procedural</u>***; you have to describe, in great detail, every step the program should take. When working with procedural languages, it is usually much harder to clearly describe the data your program will process. For this reason, `awk` programs are often refreshingly easy to read and write.
>
>   -- [GNU General Instruction for AWK](https://www.gnu.org/software/gawk/manual/gawk.html#Getting-Started)

### Offical Examples

-   [How to Run `awk` Programs](https://www.gnu.org/software/gawk/manual/gawk.html#Running-gawk)
-   [Data files for the Examples](https://www.gnu.org/software/gawk/manual/gawk.html#Sample-Data-Files)
-   [Some Simple Examples](https://www.gnu.org/software/gawk/manual/gawk.html#Very-Simple)
-   [An Example with Two Rules](https://www.gnu.org/software/gawk/manual/gawk.html#Two-Rules)
-   [A More Complex Example](https://www.gnu.org/software/gawk/manual/gawk.html#More-Complex)
