---
title: "My Vim Learning Diary 2"
date: "2023-11-13"
tags: ["Vim", "Vim Diary", "Vim Moiion", "Keybinding"]
tags: ["Vim"]
---

## Vim Motion / Keybinding

Here I will keep some of the vim motion & keybinding. (meanwhile I will keep updating this to remove those that I got very familiar, and add those that I found useful along the journey):

- `o/O`: add cursor above/below current line
- `==`:  fixing indentation for current line
- `=ap`: fixing indentation for current paragraph (the inner-most function-like scope structure under cursor)
- `yyp` : copy current line and paste the line below
  ```
  yyp
  # yy: yank current line into default register
  # p:  paste the default register into the next line (the line below current cursor)

- `Vyp`: copy current line and paste the line below
  ```
  Vyp
  # V:  enter visual line mode
  # y:  yank the current selected line (by default you will be selecting the current line)
  # p:  paste the default register into the next line (the line below current cursor)
  ```

- `di"`: delete inside the quotation mark (similarly there's `di[`, `di{` etc)
  ```
  di"
  # d: stands for delete
  # i: stands for inside
  # ": is the identifier, here is the quotation mark "
  ```
- `da"`: delete quotation mark and its inside cotnent (similarly there's `da[`, `da{` etc)

  ```
  da"
  # d: stands for delete
  # a: stands for all
  ```
  di"
  # d: stands for delete
  # i: stands for inside
  # ": is the identifier, here is the quotation mark "
  ```
  # ": is the identifier, here is the quotation mark "
  ```

---

## Vim Command

Here I will keep some of the vim commands (stuff run via `:`, "`Enter ⏎`"):

- `:e!`: reverting file to the last save version
- `:Ex`: exit to current file's working directory (or folder)


----

## Reference

[Vim Motions Guide (2022) - Vim Salesman](https://www.youtube.com/watch?v=hsFnJgmLOLk)
