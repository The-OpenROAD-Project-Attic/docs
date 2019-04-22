Developer Guide
===============
In order to maintain our codebase, we have identified some coding standards and practices to follow if you want to contribute to the cloud infrastructure.


Commenting & Documentation
---------------------------

You should write comments for your code especially where there is a flow logic.
When the text is that obvious, it's not productive to repeat it within comments.
You should write doc comments inside methods and functions describing inputs and outputs of that procedure.

Indentation
------------
We adopt the following conventions:
- Indentation must be with **SPACES** not tabs. The idea behind this is that tabs may change between different OSes. It may be configured as one tab = 4 spaces on Linux and configured with 8 spaces on Windows. Using spaces will make the source code readable in any platform.
- Python, JS, C/C++: should be with **4 SPACES** indentation.
- HTML and JSON: should be with **2 SPACES** indentation


Blocks
------
We adopt the following style::


    if(x > 1) {
    }


Naming Conventions
-------------------
Variables should be descriptive and contain one or more words. It should be
meaningful. We avoid names such as lst, x, y ... etc.
There are two ways of naming; camelCase or underscores. Below are how we suggest naming for each language:

- JavaScript => camelCase (Variables, Functions, Methods).
- Python => underscores (Variables, Functions, Methods).
- Classes use a capital letter for each word such as `RuleType`.
- Classes **must** be singular.
- We favor readability over brevity.
- We Avoid using identifiers that conflict with keywords of widely used programming languages.


Imports Order
--------------
We group imports such that:

- Built-in packages are on the top and first section.
- Framework related packages comes in the second section.
- Your packages, classes and modules comes in the third section.


Operators and Line length
-------------------------
- Operators should be surrounded by spaces such that `variables = 12`
- No line of code should exceed **79 characters**. Our eyes are more comfortable when reading tall and narrow columns of text. This is precisely the reason why newspaper articles are organized in columns.


DRY & DIE Principle
--------------------
DRY stands for *Don't Repeat Yourself*. Also, known as DIE: *Duplication Is Evil*.
The principle states that:

**Every piece of knowledge must have a single, unambiguous, authoritative representation within a system.**

File and Folder Organization
-----------------------------
Technically, we could write an entire application code within a single file.
But that would prove to be a nightmare to read and maintain. As applications grow, the file also becomes huge and unmaintainable.

**We always try to minimize lines of code per file.**

No hard-coding
-----------------
We do not hard-code anything that can be changed in the future, rather we try to put it in a separate setting or constant file.

- No hard-code URLs.
- No hard-code DB connection configuration.
- No hard-code email configuration.

