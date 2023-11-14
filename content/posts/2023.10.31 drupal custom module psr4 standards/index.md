---
title: "Drupal custom module (PSR4) standard"
summary: "[Drupal Custom Module] PHP PSR Standards"
date: 2023-10-31
---

---
- ## PSR-1: Basic Coding Standard

    **Naming Conventions**

    Classes: `StudlyCaps`

    ```
    class ClassName {
        // ...
    }
    ```

    Methods: `camelCase`

    ```
    class ClassName {
        public function methodName() {
            // ...
        }
    }
    ```

    Constants: `UPPER_CASE_WITH_UNDERSCORES`

    ```
    class ClassName {
        const CONSTANT_NAME = 'value';
    }
    ```

    ## PSR-2: Coding Style Guide

    Coding Styling:

    -   Indentation: `4 spaces`(as the tab)
    -   Opening brances for new class: `on the new line`
    -   Control structure should be followed by: `single space` (if / else / while)
    -   Function structure should: `not have space` (after the function name)

    ```
    class ClassName
    {
        public function methodName($arg1, $arg2)
        {
            if ($arg1 === $arg2) {
                return true;
            } else {
                return false;
            }
        }
    }
    ```

    ## PSR-4: Autoloading Standard

    PSR-4 is a modern autoloading standard that simplifies the process of including PHP files in your codebase. It requires:

    -   A one-to-one relationship between **class names** and **file paths**.
    -   **Namespace** declarations to match the **directory structure**.

    ```
    // -------------------------------------------
    // File: src/ExampleNamespace/ExampleClass.php
    
    namespace ExampleNamespace;
    
    class ExampleClass
    {
        // ...
    }
    
    // -------------------------------------------
    // Usage of the ExampleClass.php File
    
    require 'vendor/autoload.php';
    
    use ExampleNamespace\ExampleClass;
    
    $example = new ExampleClass();
    ```

    Reference: https://reintech.io/blog/php-and-psr-standards-writing-clean-and-compatible-php-code