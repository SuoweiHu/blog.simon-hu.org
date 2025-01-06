---
title: "Shell Assign Command Output to Varibale"
date: "2024-02-13"
tags: ["Terminal"]
---

## Usage

In case you want to have the output of a command in the CLI in bash or zsh saved into a variable, you can do that via the following:
```
variable_name____=$(your_command_here)
npm_package_list_=$(npm list -g &> /dev/null)
admin_username___=$(ahoy drush uinf --uid=1 --fields=name --format=string)
```

And you can re-use these variables in the command like, for example
```
admin_username=$(ahoy drush uinf --uid=1 --fields=name --format=string)
ahoy drush uublk $admin_username
ahoy login
```

## Reference

- [https://stackoverflow.com/questions/16967982/zsh-shell-how-to-assign-something-to-a-variable-quietly](https://stackoverflow.com/questions/16967982/zsh-shell-how-to-assign-something-to-a-variable-quietly)