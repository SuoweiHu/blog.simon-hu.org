---
title: "✅ Dart Sass ❌ LibSass ❌ Ruby-Sass "
date: "2024-05-02"
tags: ["CSS"]
---



## TL;DR

**Dart Sass**

-   **<u>Active maintenance/development</u>**
-   Dart Sass is 5-10x **faster** than Ruby Sass and only about 1.5x slower than LibSass.
-   Dart is **easy to work with** + JavaScript compatibility
-   Dart is **garbage collected** (unlike LibSass which is written in C++)

**LibSass (Node Sass)**

-   **<u>Deprecated on 2019-Mar-26;</u>**

-   LibSass’s low-level language makes it substantially **harder to add new features**
-   LibSass’s feature surface was **static** in practice (no one is developing new feature in the community)
-   LibSass does **not support some feature** that was even supported in native css (such as `min()` and `max()`)

**Ruby Sass**

-   **<u>Deprecated on 2020-Oct-26;</u>**
-   Ruby Sass was far **too** **slow** for use cases involving large stylesheets





## Why using <u>Dart Sass</u> instead ?

**Why Re-written ?**

>   Over the past few years, there have been two primary implementations of Sass. [Ruby Sass](https://github.com/sass/sass) was the original, written mostly by me with substantial help from [Chris](https://twitter.com/chriseppstein). It’s high-level and easy to hack on, so it’s where we iterate on new features and where they first get released. Then there’s [LibSass](https://github.com/sass/libsass), the C++ implementation, originally created by [Aaron](https://github.com/akhleung) and [Hampton](https://github.com/hamptonmakes) and now maintained by [Marcel](https://github.com/mgreter) and [Michael](https://github.com/xzyfer). It’s low-level, which makes it very fast and easy to install and embed in other languages. In particular, its [Node.js bindings](https://github.com/sass/node-sass) are a very popular way to use Sass in the JavaScript world.
>
>   Each implementation’s strengths complement the other’s weaknesses. Where LibSass is fast and portable, Ruby Sass is slow and difficult for non-Ruby-users to install. Where Ruby Sass is easy to iterate on, **LibSass’s low-level language makes it substantially harder to add new features**. A complementary relationship can be healthy, but it can also mean that neither solution is as good as it needs to be. That’s what we found when, in May, [Marcel officially left the LibSass team](https://sass-lang.com/blog/thank-you-marcel/)[[1\]](https://sass-lang.com/blog/announcing-dart-sass/#fn1).
>
>   Without two people’s worth of effort, we were no longer sure that LibSass could keep pace with the speed Chris and I wanted to introduce changes into the language. And it had been clear for a long time that **Ruby Sass was far too slow for use cases involving large stylesheets**. We needed a new implementation, one that could generate CSS quickly *and* add new features quickly.
>
>   -- **[Announcing Dart Sass: Why Rewrite Sass?](https://sass-lang.com/blog/announcing-dart-sass/)** - sass-lang.com

**Why using Dart ?**

>   We considered a number of possible languages, and ended up deciding on Dart for a number of reasons. First, it’s *really fast*—the Dart VM is generally much faster than JavaScript VMs, and [early benchmarks](https://github.com/sass/dart-sass/blob/main/perf.md)[[2\]](https://sass-lang.com/blog/announcing-dart-sass/#fn2) indicate that, for large stylesheets, **Dart Sass is 5-10x faster than Ruby Sass and only about 1.5x slower than LibSass**. I’ll hazard a guess that it would be about 1.5-2x faster than an idiomatic JS implementation, but I can’t say for sure. And Dart’s performance continues to get better all the time.
>
>   At the same time, **Dart is easy to work with**—much more so than C++, and to some extent even more than Ruby for such a large project. Granted, not as many people are familiar with it as with **JavaScript**, but language implementations don’t tend to get many external contributions anyway. I’ll be doing most of the work on the new implementation, and Dart is the language that I’m personally most comfortable with at the moment (when I’m not working on Sass, I’m on the Dart team). Using Dart gives me a lot of extra velocity.
>
>   Unlike Ruby or JavaScript, Dart is *statically typed*, so every value’s type can be figured out without running the code. Unlike C++, it’s ***garbage collected***, so we don’t have to worry as much about cleaning up after ourselves. This makes it easy to write, easy to modify, and easy to maintain. Maybe even more importantly, it makes it easy to translate to other programming languages, which will help LibSass get new features faster.
>
>   The last reason we chose Dart is something that only a few other languages can boast: **JavaScript compatibility**. Dart can be compiled to JavaScript, which can be used directly in Node.js or even potentially run in a browser. A huge chunk of the Sass ecosystem built on node-sass, and we intend to make the JS version of Dart Sass as close to API-compatible with node-sass as possible, so that it can easily drop into existing tools and build systems.
>
>   The **only downside is that there’s a speed hit**: Dart Sass is about twice as slow running on V8 as it is running on the Dart VM. However, this still puts it solidly 3-4x faster than Ruby Sass. Ultimately we also hope to provide an easy path for users of the JS-compiled version to move to the Dart VM version as little friction as possible.
>
>   -- **[Announcing Dart Sass: Why Dart?](https://sass-lang.com/blog/announcing-dart-sass/#why-dart)** \- sass-lang.com <u>(Posted 31 October 2016 by Natalie Weizenbaum)</u>







## Deprecation of <u>Ruby Sass</u>

**When is the deprecation ?**

>   Ruby Sass was the original implementation of Sass, but it reached its end of life as of **26 March 2019**. It’s no longer supported, and Ruby Sass users should migrate to another implementation.
>
>   **-- [Ruby Sass: But Why?](https://sass-lang.com/ruby-sass/)** - sass-lang.com

**Why perform the deprecation ?**

>   When Natalie and Hampton first created Sass in 2006, Ruby was the language at the cutting edge of web development, the basis of their already-successful [Haml](https://haml.info/) templating language, and the language they used most in their day-to-day work. Writing Sass in Ruby made it readily available to their existing users and the whole booming Ruby ecosystem.
>
>   Since then, Node.js has become ubiquitous for frontend tooling while Ruby has faded into the background. At the same time, Sass projects have grown far larger than we initially envisioned them, and their **performance needs have outpaced the speed Ruby can provide**. Both [Dart Sass](https://sass-lang.com/dart-sass) and [LibSass](https://sass-lang.com/libsass) are blazing fast, easy to install, and are readily available on npm. Ruby Sass couldn’t keep up, and it didn’t make sense to spend the core team’s resources on it any longer.
>
>   **-- [Ruby Sass: But Why?](https://sass-lang.com/ruby-sass/)** - sass-lang.com







## Deprecation of <u>LibSass</u> and <u>Node Sass</u>

**What does this mean ?**

>    After much discussion among the Sass core team, we’ve come to the conclusion that it’s time to officially declare that **LibSass and the packages built on top of it, including Node Sass, are deprecated**. For several years now, it’s been clear that there’s simply not enough engineering bandwidth behind LibSass to keep it up-to-date with the latest developments in the Sass language (for example, the most recent new language feature was added in [November 2018](https://github.com/sass/libsass/releases/tag/3.5.5)). As much as we’ve hoped to see this pattern turn around, even the excellent work of long-time LibSass contributors Michael Mifsud and Marcel Greter couldn’t keep up with the fast pace of language development in both CSS and Sass.
>
>   I'll go into detail about what this means below, but here are the major points:
>
>   -   We **no longer recommend LibSass** for new Sass projects. Use [Dart Sass](https://sass-lang.com/dart-sass) instead.
>   -   We recommend all **existing LibSass users make plans to eventually move onto Dart Sass**, and that all Sass libraries make plans to eventually drop support for LibSass.
>   -   We’re **no longer planning to add any new features** to LibSass, including compatibility with new CSS features.
>   -   LibSass and Node Sass will **continue to be maintained** indefinitely on a best-effort basis, including fixing major bugs and security issues and maintaining compatibility with the latest Node versions.
>
>   -- [**LibSass is Deprecated**](https://sass-lang.com/blog/libsass-is-deprecated/) \- sass-lang.com

**Why deprecation ?**

>   For several years now, Sass has managed to exist in an ambiguous kind of state where LibSass was an officially-supported implementation in theory, but its **feature** **surface was static in practice**. As time has gone on, it’s becoming increasingly clear that this state causes substantial concrete problems for Sass users. For example, we regularly see users confused as to why [plain-CSS `min()` and `max()` don’t work](https://github.com/sass/sass/issues/2849) and assuming Sass as a whole is at fault, when in fact it’s only LibSass that **doesn’t support that feature**.
>
>   Official support for LibSass doesn’t just cause pain for individual users. Because LibSass **doesn’t support the [Sass module system](https://sass-lang.com/blog/the-module-system-is-launched)** that launched last year, major shared Sass libraries have been unable to use it for fear that their downstream users would be incompatible. By clearly indicating that all Sass users should eventually move off of LibSass, we hope to make it more feasible for these library authors to use more modern features.
>
>   LibSass has even inhibited the development of the Sass language itself. We’ve been unable to move forward with the proposal for [treating `/` as a separator](https://github.com/sass/sass/blob/main/accepted/slash-separator.md) because any code they’d write would either produce deprecation warnings in Dart Sass or fail to compile in LibSass. By marking LibSass as deprecated, this becomes much more feasible, and Sass becomes much better at supporting the latest versions of CSS.
>
>   -- [**LibSass is Deprecated**](https://sass-lang.com/blog/libsass-is-deprecated/) \- sass-lang.com





## Reference

-   **Ruby Sass Deprecation**: https://sass-lang.com/ruby-sass/
-   **LibSass is Deprecated**:  https://sass-lang.com/blog/libsass-is-deprecated/
-   **Announcing Dart Sass:**  https://sass-lang.com/blog/announcing-dart-sass/#why-dart



