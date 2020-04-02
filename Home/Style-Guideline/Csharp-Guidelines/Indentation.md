[[_TOC_]]

Indentation is constructed with tabs, not spaces. Typically, tabs are set to be displayed as white space with a width of four characters.

# Line Length

Optimizing for down level tools and editors such as Notepad should not impact code style. 80 character lines are a recommendation, not a hard and fast rule.

# Wrapping Lines

When an expression will not fit on a single line, break it according to these general principles:

* Break after an operator.

* Break after a comma.

* Prefer higher-level breaks to lower-level breaks.

* Indent once after a break.

Here is an example of breaking a method call:

```
SomeMethod1(longExpression1, someMethod2(longExpression2,
     longExpression3)); // Note: 1 indent start second line.
```

Following are two examples of breaking an arithmetic expression. The first is preferred, since the break occurs outside the parenthesized expression, which is at a higher level.

```
longName1 = longName2 * (longName3 + longName4 - longName5) +
    4 * longname6; // PREFER

longName1 = longName2 * (longName3 + longName4
    - longName5) + 4 * longname6; // AVOID
```

Following is an example of indenting method declarations:

```
SomeMethod(int anArg,
    Object anotherArg,
    String yetAnotherArg,
    Object andStillAnother)
{
 ...
}
```

Line wrapping for if statements should use the indent rule. For example: 

```
// USE THIS INDENTATION
if ((condition1 && condition2) ||
    (condition3 && condition4) ||
    !(condition5 && condition6))
{
    DoSomethingAboutIt();
}

// OR USE THIS
if ((condition1 && condition2) || (condition3 && condition4) ||
    !(condition5 && condition6))
{
    DoSomethingAboutIt();
}
```

Here are two acceptable ways to format ternary expressions:

```
alpha = (aLongBooleanExpression ? beta : gamma);

alpha = (aLongBooleanExpression ?
    beta :
    gamma); 
```