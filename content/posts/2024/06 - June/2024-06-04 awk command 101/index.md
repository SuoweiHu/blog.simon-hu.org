---
title: "Awk command 101"
date: "2024-06-04"
tags: ["CLI", "Linux"]
---



---

**[PENDING - YouTube Series about AWK command](https://www.youtube.com/watch?v=I-uWvNvtJcY&list=PLY-V_O-O7h4fzqbPT0kpQMl8XlPvSse9H)**








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

### Offical Examples

-   [How to Run `awk` Programs](https://www.gnu.org/software/gawk/manual/gawk.html#Running-gawk)
-   [Data files for the Examples](https://www.gnu.org/software/gawk/manual/gawk.html#Sample-Data-Files)
-   [Some Simple Examples](https://www.gnu.org/software/gawk/manual/gawk.html#Very-Simple)
-   [An Example with Two Rules](https://www.gnu.org/software/gawk/manual/gawk.html#Two-Rules)
-   [A More Complex Example](https://www.gnu.org/software/gawk/manual/gawk.html#More-Complex)



















---

## Terminologies

### Data Source

#### Record

-   **Record refers to a <u>basic unit</u> of data, that `awk` is able to <u>process at a single operation</u>.**
-   By default, each line in a file or input stream is considered a record; Seprated using the `RS` built-in varaible which by default is `\n`).

#### Field

-   **Field referes to a <u>sub-unit of data</u> that are contained in a record, that `awk` is able to <u>match pattern</u> or <u>execute action</u> on.**
-   By default, each word divided by space or tabs is considered a field; Seprated using `FS` built-in variable which by default is `\t` or `space`; and you can set it to something else like `,` to handle `csv` data input (refer to the "Built-in Variable Section")

### Patter/Action

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
























---

## Command Baisc

### Primitive Form

>   (for this section, we will use [person-info](./person-info) as our data source)

In awk's simplest form, the command can be used to perform action alone (`awk '{action}' input_file`); Or match a certain pattern, then perform actions only  on the matching lines (`awk '/regex_pattern/{action}' input_file`):

```
>   awk '{print $0}' person-info
-|  fristName       lastName        age     city       ID
-|
-|  Thomas          Shelby          30      Rio        400
-|  Omega           Night           45      Ontario    600
-|  Wood            Tinker          54      Lisbon     N/A
-|  Giorgos         Georgiou        35      London     300
-|  Timmy           Turner          32      Berlin     N/A
```

```
>   awk '/N\/A/{print $0}' person-info   #pattern is "N/A"
-|  Wood            Tinker          54      Lisbon     N/A
-|  Timmy           Turner          32      Berlin     N/A
```



### Action - Built-in Variable

>   (for this example, we will use [employee.txt](./employee.txt) as our data source)

You might have noticed in the previous example, we have used `'{print $0}'` as the action of the `awk` command to print out the whole line when matched, in this action, the `$0` is a build-in variable. Similarly we have:

```
$1, $2, $3, ... :           to represent the individual fields/words seprated by seprator
$0:                         to represent the entire line
NR:  (NumberRow)            current count of the number of input records (this is usually used as "line numbers")
NF:  (NumberField)          count of the number of fields within the current input record
FS:  (FieldSeprator)        field separator character which is used to divide fields on the input line. (The default is “white space”)
RS:  (RecordSeprator)       current record separator character (the default record separator character is a newline)
OFS: (OutputFieldSeprator)  similar to FS but for output of awk command
ORS: (OutputRecordSeprator) similar to RS but for output of awk command

```

And you are able to change these built-in variables via either (using `FS` as example):

-   **<u>Environmental variable</u>**: `awk -v FS=',' '{ print $1, $2 }' filename`
-   **<u>Inline setting</u>**: `awk -F, '{ print $1, $2 }' filename`
-   **<u>BEGIN block setting</u>**: `awk 'BEGIN { FS = "," } { print $1, $2 }' filename`



### Action - Program from file

As the previous examples demonstrated, it is easy to perform AWK command with **<u>short</u>** pattern and action inline

```
>         awk '{ print "Hello" }'
> stdout: Hello
```

But when the pattern and action gets **<u>long</u>**, you mihgtmight want to have them in a **<u>separate source file</u>**:

```
>         echo 'BEGIN { print "Dont Panic" }' > awk_src.txt && ls
> stdout: -rw-r--r--    1 root  staff    29 Jun  4 11:32 awk_src.txt
> stdout: -rw-r--r--    1 root  staff    29 Jun  4 11:32 ..
>
>         awk -f ./awk_src.txt
> stdout: Don Panic
```



### Pattern - Regex Patterns

>   (for this secion, we will use [mail-list ](./mail-list)as our data source)

You can check if a certain pattern have appeared:

```
$  awk "/samuel.lanceolis@shu.edu/" mail-list
-| Samuel       555-3430     samuel.lanceolis@shu.edu        A
```

You can perform **<u>matching operation on one column</u>** and <u>**print out a different column**</u>:

```
$  awk '$1=="Samuel" { print $3 }' mail-list
-| samuel.lanceolis@shu.edu
```

You can perform **<u>logical operations</u>** (`&&` / `||` / `!`) on the regular expression like you would do on other programming language:

```
$  awk '/edu/ && /555/' mail-list                #AND
-| Fabius       555-1234     fabius.undevicesimus@ucb.edu    F
-| Samuel       555-3430     samuel.lanceolis@shu.edu        A
-| Jean-Paul    555-2127     jeanpaul.campanorum@nyu.edu     R
```

```
$  awk '/edu/ || /gmail/' mail-list              #OR
-| Amelia       555-5553     amelia.zodiacusque@gmail.com    F
-| Becky        555-7685     becky.algebrarum@gmail.com      A
-| Fabius       555-1234     fabius.undevicesimus@ucb.edu    F
-| Samuel       555-3430     samuel.lanceolis@shu.edu        A
-| Jean-Paul    555-2127     jeanpaul.campanorum@nyu.edu     R
```

```
$  awk '!/edu/ && !/hotmail/ && !/gmail/' mail-list      #NOT
-| Broderick    555-0542     broderick.aliquotiens@yahoo.com R
-| Camilla      555-2912     camilla.infusarum@skynet.be     R
-| Julie        555-6699     julie.perscrutabor@skeeve.com   F
```



















---

## Command Input Options

### input from stdin/stdout

You can use awk command to perform actions on your **<u>standard input</u>**

```
>         awk '/How are you?/ { print "Im fine, thank you" }'
> stdin:  How are you?           # input that matches the pattern
> stdout: Im fine, thank you     # action that is specified by user
> stdin:  Random gibberish       # input that does not match
> stdout: (null)                 # no action performed
```

You can also use awk command to perform action on your <u>**standard output**</u>

```
>         echo "How are you? Man?" | awk '/How are you?/ { print "Im fine, thank you" }'
> stdout: Im fine, thank you
>
>         echo "How is your uncle?" | awk '/How are you?/ { print "Im fine, thank you" }'
> stdout: (null)
```

### input from file

For instance you have the following file ([employee-1.txt](./employee-1.txt), [employee-2.txt](./employee-2.txt)):

```txt
ajay manager account 45000
sunil clerk account 25000
varun manager sales 50000
amit manager account 47000
```

```
tarun peon sales 15000
deepak clerk sales 23000
sunil peon sales 13000
satvik director purchase 80000
```

You can then filter their content, via pattern `sales` (check if it appears in any of the line):

```
>         awk 'sales' employee-1.txt
> stdout: varun manager sales 50000
>
>         awk 'sales' employee-2.txt
> stdout: tarun peon sales 15000
> stdout: deepak clerk sales 23000
> stdout: sunil peon sales 13000
>
>         awk 'sales' employee-1.txt employee-2.txt
> stdout: varun manager sales 50000
> stdout: tarun peon sales 15000
> stdout: deepak clerk sales 23000
> stdout: sunil peon sales 13000
```

###





















---

## Reference

-   [GNU Command Manual - GAWK](https://www.gnu.org/software/gawk/manual/gawk.html#Getting-Started)
-   [GeeksForGeeks - AWK command in Unix/Linux with examples](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)
-   [FreeCodeCamp - The Linux AWK Command](https://www.freecodecamp.org/news/the-linux-awk-command-linux-and-unix-usage-syntax-examples/#:~:text=The%20Basic%20Syntax%20of%20the,to%20search%20through%20mentioned%20last)
-   [NextGen Learning - AWK Basics](https://www.youtube.com/watch?v=I-uWvNvtJcY&list=PLY-V_O-O7h4fzqbPT0kpQMl8XlPvSse9H)