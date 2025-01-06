---
title: "Regular Expression 101"
date: 2024-08-05
tags: ["Terminal"]
---



## Regular Expression Tester

[**Regular Expressions 101**](https://regex101.com/)

-   Example match: [screenshot](2024-08-05T140308.jpg)
-   Example mis-match: [screenshot](2024-08-05T140353.jpg)





## CheatSheet

-   **[DataScienceDojo Cheatsheet - IMAGE](2024-08-05T135526.jpg)**

-   **[DataCamp Cheatsheet - IMAGE](image_adc9709454.png)**





## Breakdown

#### Square Brackets (`[]`)

The name might sound scary, but it is nothing but the symbol: []. Some people also refer to square brackets as character class – a regular expression jargon word that means that it will match any character inside the bracket.

For instance:

| **Pattern**  | **Matches**                 |
| ------------ | --------------------------- |
| [Pp]enguin   | Penguin, penguin            |
| [0123456789] | (This will match any digit) |
| [0oO]        | 0, o, O                     |

#### Disjunction (`|`)

The pipe symbol means nothing but either ‘A’ or ‘B’, and it is helpful in cases where you want to select multiple strings simultaneously. For instance:

| **Pattern**        | **Matches**                |
| ------------------ | -------------------------- |
| A\|B\|C            | A, B, C                    |
| Black\|White       | Black, White               |
| [Bb]lack\|[Ww]hite | Black, black, White, white |

#### Question Mark (`?`)

The question mark symbol means that the character it comes after is optional. For instance:

| **Pattern** | **Matches**   |
| ----------- | ------------- |
| Ab?c        | Ac, Abc       |
| Colou?r     | Color, Colour |

#### Asterisk (`*`)

The asterisk symbol matches with 0 or more occurrences of the earlier character or group. For instance:

| **Pattern** | **Matches**                                                  |
| ----------- | ------------------------------------------------------------ |
| Sh*         | (0 or more of earlier character h)S, Sh, Shh, Shhh.          |
| (banana)*   | (0 or more of earlier banana. This will also match with nothing, but most regex engines will ignore it or give you a warning in that case)banana, bananabanana, bananabananabanana. |

#### Plus (`+`)

The plus symbol means to match with one or more occurrences of the earlier character or group. For instance:

| **Pattern** | **Matches**                                                  |
| ----------- | ------------------------------------------------------------ |
| Sh+         | (1 or more of earlier character h)Sh, Shh, Shhh.             |
| (banana)+   | (1 or more of the earlier banana)banana, bananabanana, bananabananabanana. |

#### Negation (`^`)

Negation has two everyday use cases:

1.   Inside square brackets, it will search for the negation of whatever is inside the brackets. For instance:

| **Pattern**   | **Matches**                                    |
| ------------- | ---------------------------------------------- |
| [^Aa]         | It will match with anything that is not A or a |
| [^0123456789] | It will match anything that is not a digit     |

2.   It can also be used as an anchor to search for expressions at the start of the line(s) only. For instance:

| **Pattern**      | **Matches**                                                  |
| ---------------- | ------------------------------------------------------------ |
| ^Apple           | It will match with every Apple that is at the start of any line in the text |
| ^(Apple\|Banana) | It will match with every Apple and Banana that is at the start of any line in the text |

#### Dollar (`$`)

A dollar is used to search for expressions at the end of the line. For instance:

| **Pattern**   | **Matches**                                                  |
| ------------- | ------------------------------------------------------------ |
| $[0123456789] | It will match with any digit at the end of any line in the text. |
| $([Pp]anda)   | It will match with every Panda and panda at the end of any line in the text. |







## Reference

-   https://datasciencedojo.com/blog/regular-expression-101/

-   https://www.datacamp.com/cheat-sheet/regular-expresso