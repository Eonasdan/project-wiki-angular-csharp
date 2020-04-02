[[_TOC_]]

# Simple Statements

Each line should contain at most one statement. Example:

```
argv++; // Correct
argc--; // Correct
argv++; argc--; // AVOID!
```

# Compound Statements

Compound statements are statements that contain lists of statements enclosed in braces "`{ statements }`". See the following sections for examples.

* The enclosed statements should be indented one more level than the compound statement.

* The opening brace should be at the beginning of the line following the line that begins the compound statement and be indented to the beginning of the compound statement. The closing brace should begin a line and be indented to the beginning of the compound statement.

* Braces are used around all statements, even single statements, when they are part of a control structure, such as a if-else or for statement. This makes it easier to add statements without accidentally introducing bugs due to forgetting to add braces.

# return Statements

A `return` statement with a value should not use parentheses unless they make the return value more obvious in some way. Example:

```
return;

return myDisk.size();

return (size ? size : defaultSize);
```

# if, if-else, if else-if else Statements

The `if-else` class of statements should have the following form:

```
if (condition)
{
    statements;
}

if (condition)
{
    statements;
}
else
{
    statements;
}

if (condition)
{
    statements;
}
    else if (condition)
{
    statements;
}
else
{
    statements;
}
```

<div class="alert alert-info">
    Single statement `if-statements` are permitted <strong>if</strong> it is clear what the code does and show be placed on a single line if possible.
</div>

# for Statements

A `for` statement should have the following form:

```
for (initialization; condition; update)
{
    statements;
}
```

# while Statements

A `while` statement should have the following form: 

```
while (condition)
{
    statements;
}
```

An empty `while` statement should have the following form:

```
while (condition);
```

# do-while Statements

A `do-while` statement should have the following form:

```
do
{
    statements;
} while (condition);
```


## switch Statements
A switch statement should have the following form:

```
switch (condition)
{
    case 1:
        // Falls through.
    case 2:
        statements;
        break;
    case 3:
        statements;
        goto case 4;
    case 4:
        statements;
        break;
    default:
        statements;
        break;
}
```

When there is no code between two cases and there is no `break` statement, the code falls though. If `case 1` is satisfied, the code for `case 2` will execute. If code is present between two cases, and a fall through is desired, a `goto case` statement is required, as in `case 3`. This is done so that errors aren't introduced by inadvertently omitting a break.

## try-catch Statements

A try-catch statement should have the following format:

```
    try
    {
        statements;
    }
    catch (ExceptionClass e)
    {
        statements;
    } 
```

A `try-catch` statement may also be followed by finally, which executes regardless of whether or not the try block has completed successfully.

```
try
{
    statements;
}
catch (ExceptionClass e)
{
    statements;
}
finally
{
    statements;
} 
```