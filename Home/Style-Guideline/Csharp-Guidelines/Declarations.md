[[_TOC_]]

# Number Per Line

One declaration per line is recommended since it encourages commenting. In other words,

```
private int _level = 2; // indentation level
private int _size = 8; // size of table
```

is preferred over

```
private int level, size; // AVOID!!!
```

# Initialization

Try to initialize local variables where they're declared. The only reason not to initialize a variable where it's declared is if the initial value depends on some computation occurring first. For instance, if you declare an int without initializing it and expect a public method of the owning class to be invoked that will act on the in, you will have no way of knowing if the int was properly initialized for it was used. In this case declare the int and initialize it with an appropriate value.

## Placement

Put declarations only at the beginning of blocks. (A block is any code surrounded by curly braces "`{`" and "`}`".) Don't wait to declare variables until their first use; it can confuse the unwary programmer and hamper code portability within the scope.

```
public void SomeMethod()
{
    int int1 = 0; // Beginning of method block.
    if (condition)
    {
        int int2 = 0; // Beginning of "if" block.
        ...
    }
}
```

The one exception to the rule is indexes of for loops, which in C# can be declared in the for statement:

```
for (int i = 0; i < maxLoops; i++)
{
// Do something
}
```

# Class and Interface Declarations

When coding C# classes and interfaces, the following formatting rules should be followed: 

* No space between a method name and the parenthesis "`(`" starting its parameter list

* Open brace "`{`" appears at the beginning of the line following declaration statement and is indented to the beginning of the declaration.

* Closing brace "`}`" starts a line by itself indented to match its corresponding opening statement. For null statements, the "`}`" should appear immediately after the "`{`" and both braces should appear on the same line as the declaration with 1 blank space separating the parentheses from
the braces:

```
public class Sample : Object
{
    private int ivar1;
    private int ivar2;

    public Sample(int i, int j)
    {
        this.ivar1 = i;
        this.ivar2 = j;
    }

    protected void EmptyMethod() {}
}
```

* Methods are separated by two blank lines.

# Properties

If the body of the get or set method of a property consists of a single statement, the statement is written on the same line as the method signature. White space is inserted between the property method (get, set) and the opening brace. This will create visually more compact class definitions...

```
public int Foo
{
    get { return this.foo; }
    set { this.foo = value; }
}
```

instead of

```
public int Foo
{
    get
    {
        return this.foo;
    }
    set
    {
        this.foo = value;
    }
} 
```