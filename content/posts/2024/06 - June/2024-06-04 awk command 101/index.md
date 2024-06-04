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





## Terminologies 

### Data Source 

#### Record

-   **Record refers to a <u>basic unit</u> of data, that `awk` is able to <u>process at a single operation</u>.** 
-   By default, each line in a file or input stream is considered a record; Seprated using the `RS` built-in varaible which by default is `\n`).

#### Field

-   **Field referes to a <u>sub-unit of data</u> that are contained in a record, that `awk` is able to <u>match pattern</u> or <u>execute action</u> on.** 
-   By default, each word divided by space or tabs is considered a field; Seprated using `FS` built-in variable which by default is `\t` or `space`; and you can set it to something else like `,` to handle `csv` data input (refer to the "Built-in Variable Section")



### Patter/Action

>   When you run `awk`, you specify an `awk` *program* that tells `awk` what to do. The program consists of a series of*rules* (it may also contain *function definitions*, an advanced feature that we will ignore for now; see [User-Defined Functions](https://www.gnu.org/software/gawk/manual/gawk.html#User_002ddefined)). Each rule specifies **<u>one pattern to search</u>** for and **<u>one action to perform</u>** upon finding the pattern.
>
>   Syntactically, a rule consists of a *pattern* followed by an *action*. The action is enclosed in braces to separate it from the pattern. Newlines usually separate rules. Therefore, an `awk` program looks like this:
>
>   ```
>   pattern { action }
>   pattern { action }
>   ...
>   ```
>
>   -- [GNU General Instruction for AWK](https://www.gnu.org/software/gawk/manual/gawk.html#Getting-Started)

#### Pattern

-   **Pattern refer to the condition/rules used by `awk`to <u>determine which record are selected</u> for processing.**

-   The pattern can be: 

    -   **Regular Expression**: define regex pattern 

        (e.g.`awk '/pattern/{action}' filename`)

    -   **Relational Expression**: logical condition based on arithmetic or string comparison 

        (e.g. `awk '$1 > 100 {print $0}' filename`)

    -   **Range Pattern**: select or ignore a range of records by using range patterns with commas 

        (e.g. `awk '/start_pattern/,/end_pattern/' filename`)

    -   **BEGIN and END block:** executes before/after any records are processed. 

        (e.g.  `awk 'BEGIN {action} {regular processing} END {action}' filename`)

#### Action

-   **Action refers to a block of code/program that **`awk` **wil process matching record with**.

-   The action can be:

    -   **Print / Caculation / Assignment**

        -   **Print output**: simply use stdout to show the processed result 

            (e.g. `awk '/pattern/' {print $1, $3} filename`)

        -   **Variable Assignment**: set or change the value of variabale 

            (e.g. `awk '{ total += $1 } END { print "Total:", total }' filename`)

        -   **Arithmetic Operations**: perform calculation on field

            (e.g. `awk '{ if ($1 > 100) print $0 }' filename`)

    -   **Conditional / Loop / Array Operation**

        -   **Conditional Statment**: execute code block based on specific operation

            (e.g. `awk '{ if ($1 > 100) print $0; else print "condition not met" }' filename`)

        -   **For Loop**: iterate over the fields

            (e.g. `awk '{ for (i = 1; i <= NF; i++) print $i }' filename`)

        -   **Array Operations**: use associative arrays for storing and accessing data based on keys.

            (e.g. `awk '{ count[$1]++ } END { for (val in count) print val, count[val] }' filename`)

    -   **Functional Call**: use built-in or user-defined functions for complex tasks.

        -   built-int function example: `awk '{ print length($0) }' filename`

        -   user defined function: 

            ```
            # Define a function to compute factorial and use it
            awk 'function factorial(n) { return (n == 1 || n == 0) ? 1 : n * factorial(n-1) }
            { print factorial($1) }' filename
            ```

            



