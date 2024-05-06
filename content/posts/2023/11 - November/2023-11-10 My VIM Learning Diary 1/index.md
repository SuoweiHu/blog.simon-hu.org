---
title: "My Vim Learning Diary 1"
date: "2023-11-08"
tags: ["Vim", "Vim Diary", "Vim Tutorial", "Vim Configuration"]
categories: ["Vim"]
---

## Why do "I" want to use vim ?

### Why not VS Code ?

To begin with, I am not quite the typical teenage young boy, he who have not tried; I have been coding for more than 4 years now, and at this point I already have some of the tools of my taste.

If you'd ask for my favorite my current pick is "**VS Code**". Why? because I do not code on any particular language (hence no IDE) and I just happen to land on VS Code by accident, if I would first met "Sublime", the answer could be different.

Don't get me wrong, I do use VS Code to an extent that I am confident to add "VS Code" as my professionalist on my resume, I have constructed my own VS Code theme, my own [`settings.json`](scripts/settings.json) and [`keybindings.json`](scripts/keybinding.json), use multi-cursor and regular expression editing, and build couple of extensions for my work. I do like VS Code, but it's just there isn't seemingly too much passion in the community about excelling in VS Code.

### Drawback of VSCode

After these years of experience with VS Code, I found some of the **issues** with VS Code that is commonly found by many developers, here are some of them:

- Slow indexing speed when facing large project.
- Custom setting are not available on my colleague's laptop.
- Not available as a command-line, always-available application.
- Get stuck often, due to its extensive use of memory and synchronous operation (meantime of my editing, VS Code is running file indexing, autocomplete suggestions, calculating the context of cursor, and `git blame` for every line of code change)

So here I am, deciding to take a second look at this tool (VIM), of which I firmly deny to use at my young age (I was once so firmly believing in the theory of "**Occam's razor**", thinking all those wizards IDE/Utilities are just for those who do not have a job...).


### Why switch VIM ?

Recently I met this YouTuber [ThePrimeTimeagen](https://www.youtube.com/@ThePrimeTimeagen) which gives contentful tips about best practices being a programmer, he share his insights via reading out aloud while watching related contents (other programmers related topic videos, blog post, etc). For instance, [this one](https://www.youtube.com/watch?v=Vkk_DH4kw7U) got me real good, where one should really learn by doing stuff (the process is like "Do a little big" → "Fail" → "Struggle" → "Find a answer"), by watching the tutorial you have skipped the fail/struggle bit, hence your memory might become very weak (not to mention that the tutorial only aims for a very narrow use case like a "start server section" in "`ReadMe.md`").

Half of the ThePrimeTimeagen's video is about vim and how good it is, I was a bit cautious on how I should take in his info without getting over biased, but after watching just two videos ([this one](https://www.youtube.com/watch?v=X6AR2RMB5tE), and [this one](https://www.youtube.com/watch?v=-cn3MAovsN4&t=1s)), I was convinced...

At this point you might be expecting some dot points listing for the advantage, pros/cons for vim comparing to VS Code, but I am not here to write a post to impressive a bunch of ya, this is just a note for myself to revisit, I'll only list the reasons **I am interested into VIM** for, check it out in the upcoming section.


---

## My Reasons to Use VIM
(in case you get lost and wanna quit)

- It is COOL !!!! No one else knows how you do it and you looks like wizards !!!!
- It will run fast on any computer, and does not eats up much of the memory.
- (Why not to use lazy-vim) If you would like to use lazy-vim, you might rather use vscode with the vim extension.



---
## Reference

My current vs code configuration(if your are curious)
- Settings: [`settings.json`](scripts/settings.json)
- Keyboard Shortcuts: [`keybindings.json`](scripts/keybinding.json)
- [ThePrimeTimeagen](https://www.youtube.com/@ThePrimeTimeagen)
- [Tutorials Are KILLING Your Growth - ThePrimeTime](https://www.youtube.com/watch?v=Vkk_DH4kw7U)