---
title: "Difference of var, let, const in JavaScript"
date: "2024-05-12"
tags: ["JavaScript"]
---



## TLDR Take Away

### Method-1

(easy to practice) <u>**Always use `let` !**</u>

### Method-2

(most agreed in community) **<u>Use `const` by default, only change `const` to `let` if afterwards you find yourself in need to change/update the variable.</u>**







## TLDR Comparison

- `var`
    - Declares a variable with <u>**function-scope**</u> or **<u>globally</u>** if declared outside of a function.
    - It **<u>can be re-declared</u>** and **<u>can be updated</u>**.
- `let`
    - Declares a variable with **<u>block scope</u>** (i.e., confined to the block, statement, or expression where it is used)
    - It **<u>cannot be re-declared</u>** within the same scope, but <u>**can be updated**</u>.
- `const`
    - Similar to ﻿let in terms of **<u>block scope</u>**
    - The variables declared with ﻿const must be **<u>initialized at declaration</u>**,
    - Const varaibels **cannot be updated**, and <u>**cannot be re-declared**</u>.

(If you are really into knowing the fine difference between each keyword, there's plenty materials you can find online, I've put some of the MDN official documents in the reference section for reference purpose.)



## Potential Issue with `var`

For the following code you might be anticipating the output to be strings of every  `wizard`  in `wizards` appearing twice, but actually it is only doing output for the `wizards` interleaved with last item of `items`.

```
var wizards =  ['Merlin',    'Gandalf', ..., "Ursula"  ];
var items   =  ['Spellbook', 'Staff',   ..., "Urchins" ];

for (var item of wizards) {
	console. log(1, item);
	for (var item of items) {
		// Stuff happens...
	}
	console.log(2, item);
}
```

```
# Expected Output:
	1 Merlin
	2 Merlin
	1 Gandalf
	2 Gandalf
	1 ...
	2 ...
	1 Ursula
	2 Ursula

# Actual Output:
    1 Merlin
	2 Urchins
	1 Gandalf
	2 Urchins
	1 ...
	2 ...
	1 Ursula
	2 Urchins
```

**Why is that?**

-   This is because var is **<u>globally</u>** scoped (or **functionally scoped**), every iteration after we first declare it in in `line 4 `(as some item of the `wizards` array), it will get redeclared and overriden at `line 6`; And since it is **<u>not block scoped</u>**, when it leaves the `for` block at `line 8` it will never get poped back to the value it once was before entering the block, hence when we arrive at `line 9` it will always be the last item of the `items` array



## Reference

-   https://www.youtube.com/watch?v=pobWEaHNChY
-   https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var
-   https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let
-   https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const

