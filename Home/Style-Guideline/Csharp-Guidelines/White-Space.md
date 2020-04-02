[[_TOC_]]

# Blank Lines

Blank lines improve readability by setting off sections of code that are logically related. One blank line should always be used in the following circumstances:

* Between the local variables in a method and its first statement

* Between logical sections inside a method to improve readability

* After the closing brace of a code block that is not followed by another closing brace.

## Blank Spaces

Blank spaces should be used in the following circumstances:

* A keyword followed by a parenthesis should be separated by a space. Example:
    
```
while (true)
{
    ...
}
```

Note that a blank space should not be used between a method name and its opening parenthesis. This helps to distinguish keywords from method calls.

* A blank space should appear after commas in argument lists.

* All binary operators except "." should be separated from their operands by spaces. Blank spaces should never separate unary operators such as unary minus, increment (`++`), and decrement (`--`) from their operands. Example:
    
```
a += c + d;
a = (a + b) / (c * d);

while (d < n)
{
    n++;
}

this.PrintSize("size is " + foo + "\n");
```

* The expressions in a for statement should be separated by blank spaces. Example: `for (expr1; expr2; expr3)`