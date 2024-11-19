---
title: "Drupal Debug Trick: debug_backtrace / debug_print_backtrace - [PENDING]"
date: "2023-11-16"
tags: ["Drupal"]
---

## PENDING ...



## ORIGINAL POST ↓
I find this useful as a less memory intensive Drupal-friendly way to backtrace PHP as a one-off code snippet to temporarily drop into a troublesome location without installing modules or server-side tools:
```php
 $trace = debug_backtrace();
  $backtrace_lite = array();
  foreach( $trace as $call ) {
    $backtrace_lite[] = $call['function']."    ".$call['file']."    line ".$call['line'];
  }
  debug( $backtrace_lite, "TRACE", true );
```

It gets the backtrace into Drupal's debugging system, but strips it down to the essentials to avoid failures when massive objects are involved. For handy reference, the other keys within each row of the debug_backtrace() object are: class, object, type, args.

## Reference

- [Drupal Answers - 1](https://drupal.stackexchange.com/questions/195219/how-to-get-a-backtrace-in-drupal-without-problems-like-out-of-memory-when-huge)
- [Drupal Answers - 2](https://drupal.stackexchange.com/questions/239099/how-to-use-dddebug-backtrace-for-an-error-debugging)
- [PHP Documentation - debug_backtrace](https://www.php.net/manual/en/function.debug-backtrace.php)


## Example Screenshot

![2023.11.16 - 161209](2023.11.16%20-%20161209.jpg)

![2023.11.16 - 161203](2023.11.16%20-%20161203.jpg)