[[_TOC_]]

# One Class per File

Source files should contain one class definition per source file. Said differently, each class definition will exist within its own file. The stem of the file name must be the same name as the name used in the class declaration. For example, the class definition for a class named `Loan` will have a file name of `Loan.cs`.

Some exceptions are acceptable such as in the case where parsing JSON would result in several micro classes and thus pollute the solution.

# Ordering

C# source files have the following ordering:

* `using` statements

* `namespace` statement

* Class and interface declarations

# Namespace and Using Statements

The first non-comment lines of most C# source files is the using statements. After that, namespace statements can follow. For example:

```
using System.Data;
namespace Business.Framework;
```

Both the `using` statement and the `namespace` statement are aligned flush against the left margin. The first letter of a component in a namespace is always capitalized. If the namespace name is an acronym, the first letter only of the namespace will be capitalized, as in `System.Data.Sql`. If the acronym only has two letters, both letters are capitalized, as in `System.IO`.

# XML Documentation

Visual Studio provides for a type of documentation that the development environment is able to detect and extract to structured XML that is used to create code-level documentation that exists outside of the source code itself.

XML documentation is provided for class descriptions, methods, and properties. XML documentation should be used in all circumstances where it's available.

Refer to the detailed discussion on XML documentation in this document as well as in the documents provided with Visual Studio .NET.

# Class and Interface Declaration

Sequence | Part of Class/Interface Declaration | Notes
------------ | ------------- | -------------
1 | Class/interface documentation | 
2 | class or interface statement | 
3 | Fields | First `private`, -> `private`, -> `internal`, and -> `public`.
4 | Properties | First `private`, -> `private`, -> `internal`, and -> `public`.
4 | Constructors | First `private`, -> `private`, -> `internal`, and -> `public`.<br/>Default first, then order in increasing complexity.
5 | Methods | Methods should be grouped by functionality rather than by scope or accessibility.<br/>For example a `private` class method can be in between two `public` instance methods. The goal is to make reading and understanding the code easier. 