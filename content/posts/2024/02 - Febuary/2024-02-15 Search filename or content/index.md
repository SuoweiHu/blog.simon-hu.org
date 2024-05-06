---
title: "Find filename and file content via GREP"
date: "2024-02-14"
categories: ["CLI", "grep"]
---



## Intuition 

I was working on two projects of whcih are comparable to each other, and I found some pattern that persists in one project-A that would be helpful for the other project-B, and for that I will need to find a specific file (either through its filename or content), however I found in project-B has its majority of the directorites hidden within the docker container. 

With that pre-condition given I cannot navigate project-B's filebase using a GUI file explorer like finder, or perform global search with GUI interface like VS-code. Consequently I will have to work around the linux command line interface, and use that to find the files I need.

```
project-A            project-B 
|_src                |_src
   |_...                |_...
      |_file_name          |_file_name ?
```



## Find filename 

To find the filename via the cli, you can use the output of tree and pipe it into grep:
```
OPTION-1: tree | grep --color=always --context=10  "file_name_pattern" 
EXAMPLE:  tree | grep --color=always --context=10  "*.php"
EXPLAIN:  tree: will print out the hierachy structure of the files under current directory 
          grep: will take the ouput of the tree and filter it based on the given regular expression 
                "--color"   option will make the match highlighted in color / bold text 
                "--context" option will make the print-out contain not only the line that matches, but also the lines of its context, with the number of lines defined given argument (equivalant to "--before" and "--after")
--------
OPTION-2:  find . -type f -name "file_name_pattern" | grep "file_name_pattern"
EXAMPLE:   find . -type f -name "*.php" | grep "modifier"
EXPLAIN:   a variant of the OPTION-1
```



## Find file content

To find the file content via cli, you can use the grep by itself: 

```
OPTION:   grep -Rnw "/path/to/somewhere/" -e  "file_content_pattern"
EXAMPLE:  grep -Rnw "./src/modules/contrib" -e "*.php"
EXPLAIN:  grep: the command line utility used for searching text pattern within the file
                "-R" or "--recursive" tells grep to search recursively in all files and directoties within the specified path
                "-n" or "--number" tells grep to display the number alone with the maching lines
                "-w" or "--word" tells grep to only display result that matches the whole word, not a part of it.
                "-e" or "--expression" is used to specify a regular expression pattern
```



## Git Grep 

And it is worth mentioning, if you are working within a git directory, you can use the "`git`" version of "`grep`". "`git grep`" is aware of Git's version control system. It can search across different versions of files in the repository, taking into account branches, commits, and file history. This is particularly useful for searching within codebases and examining changes over time. "`﻿grep`" does not have this integrated Git functionality and will search files in their current state.

```
$ git grep "2024-02-*"
  ↓ 
  content/posts/2024/2024-02-07 CSS Media Query/index.md:date: "2024-02-07"
  content/posts/2024/2024-02-08 Git Another Process Seems to Be Running/index.md:date: "2024-02-08"
  content/posts/2024/2024-02-11 Photoshop White to Transparent/index.md:date: "2024-02-11"
  content/posts/2024/2024-02-11 Photoshop White to Transparent/index.md:![2024-02-12T094701AEST](2024-02-12T094701AEST.jpg)
  content/posts/2024/2024-02-12 Drupal Module Installed but is Missing/index.md:date: "2024-02-11"
  content/posts/2024/2024-02-12 Hugo PowerMod: Custom CSS /index.md:date: "2024-02-12"
  content/posts/2024/2024-02-13 Shell Assign Command Output to Varibale/index.md:date: "2024-02-13"
```





## Reference

-   [Git Grep Official Documentation](https://git-scm.com/docs/git-grep)
-   [How to find all files containing a specific text (string) on Linux?](https://stackoverflow.com/questions/16956810/how-to-find-all-files-containing-a-specific-text-string-on-linux)

















