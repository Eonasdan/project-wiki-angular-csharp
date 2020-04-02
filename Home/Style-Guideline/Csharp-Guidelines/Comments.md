[[_TOC_]]

C# programs can have two kinds of comments: implementation comments and documentation comments. Implementation comments are those found in C++, which are delimited by `/*...*/`, and `//`. Documentation comments are C# only, and are delimited by special XML tags that can be extracted to external files for use in system documentation.

Implementation comments are meant for commenting out code or for comments about the particular implementation. Doc comments are meant to describe the specification of the code, from an implementation-free perspective, to be read by developers who might not necessarily have the source code at hand.

Comments should be used to give overviews of code and provide additional information that is not readily available in the code itself. Comments should contain only information that is relevant to reading and understanding the program. For example, information about how the corresponding component is built or in what directory it resides should not be included as a comment. Discussion of nontrivial or obscure design decisions is appropriate, but avoid duplicating information that is present in (and clear from) the code. It is too easy for redundant comments to get out of date. In general, avoid any comments that are likely to get out of date as the code evolves.

> **Note**: The frequency of comments sometimes reflects poor quality of code. When you feel compelled to add a comment, consider rewriting the code to make it clearer.

Following are recommended commenting techniques:

* When modifying code, always keep the commenting around it up to date.

* Comments should consist of complete sentences and follow active language naming responsibilities (Adds the element instead of The element is added).

* At the beginning of every routine, XML documentation is used to indicate the routine's purpose, assumptions, and limitations. A boilerplate comment should be a brief introduction to understand why the routine exists and what it can do. Refer to the detailed discussion on XML documentation in this document as well as in the document provided with Visual Studio .NET.

* Avoid adding comments at the end of a line of code; end-line comments make code more difficult to read. However, end-line comments are appropriate when annotating variable declarations. In this case, align all end-line comments at a common tab stop. 

* Avoid using clutter comments, such as an entire line of asterisks. Instead, use white space to separate comments from code. XML documentation serves the purpose of delineating methods.

* Avoid surrounding a block comment with a typographical frame. It may look attractive, but it is difficult to maintain.

* Prior to deployment, remove all temporary or extraneous comments to avoid confusion during future maintenance work.

* If you need comments to explain a complex section of code, examine the code to determine if you should rewrite it. If at all possible, do not document bad code – rewrite it. Although performance should not typically be sacrificed to make the code simpler for human consumption, a balance must be maintained between performance and maintainability.

* Use complete sentences when writing comments. Comments should clarify the code, not add ambiguity.

* Comment as you code, because most likely there won't be time to do it later. Also, should you get a chance to revisit code you've written, that which is obvious today probably won't be obvious six weeks from now.

* Avoid the use of superfluous or inappropriate comments, such as humorous sidebar remarks.

* Use comments to explain the intent of the code. They should not serve as inline translations of the code.

* Comment anything that is not readily obvious in the code. This point leads to allot of subjective interpretations. Use your best judgment to determine an appropriate level of what it means for code to be not really obvious.

* To prevent recurring problems, always use comments on bug fixes and work-around code, especially in a team environment.

* Use comments on code that consists of loops and logic branches. These are kbd areas that will assist the reader when reading source code.

* Separate comments from comment delimiters with white space. Doing so will make comments stand out and easier to locate when viewed without color clues.

* Throughout the application, construct comments using a uniform style, with consistent punctuation and structure.

* Comments should never include special characters such as form-feed and backspace.

# Implementation Comment Formats

C# syntax provides for many styles of code comments. For simplicity and based on the heuristic use of comments in C#, we will use comments traditionally reserved for end of line comments and code disabling for all cases of code comments.

# Block Comments

Block comments are used to provide descriptions of files, methods, data structures and algorithms. Block comments may be used at the beginning of each file. They can also be used in other places, such as within methods. Block comments inside a function or method should be indented to the
same level as the code they describe.

A blank line to set it apart from the rest of the code should precede a block comment.

```
// Here is a block comment 
// that breaks across multiple
// lines.
```

# Single-Line Comments

Short comments can appear on a single line indented to the level of the code that follows. If a comment can't be written in a single line, it should follow the block comment format. A single-line comment should be preceded by a blank line. Here's an example of a single-line comment in code.

```
if (condition)
{
    // Handle the condition.
    ...
}
```

# Trailing Comments

Very short comments can appear on the same line as the code they describe, but should be shifted far enough to separate them from the statements. If more than one short comment appears in a chunk of code, they should all be indented to the same tab setting.

Here's an example of a trailing comment in C# code:

```
if (a == 2)
{
    return true; // Special case
}
else
{
    return isPrime(a); // Works only for odd a
}
```

# Code-Disabling Comments

The `//` comment delimiter can comment out a complete line or only a partial line. Code-disabling comment delimiters are found in the first position of a line of code flush with the left margin. Visual Studio .NET provides for bulk commenting by selecting the lines of code to disable and pressing <kbd>CTRL</kbd>+<kbd>K</kbd>, <kbd>CTRL</kbd>+<kbd>C</kbd>. To uncomment, use the <kbd>CTRL</kbd>+<kbd>K</kbd>, <kbd>CTRL</kbd>+<kbd>U</kbd> chord.

## Important!

> Code-disabling comments should not be used to remove a feature. That's what Source Control is for. Using code-disabling comments to temporary disable code sections is permissible, but should be removed as soon as possible.

The following is an example of code-disabling comments:

```csharp
if (foo > 1)
{
    // Do a double-flip.
    ...
}
else
{
    return false; // Explain why here.
}
// if (bar > 1)
// {
//
// // Do a triple-flip.
// ...
// }
// else
// {
// return false;
// } 
```