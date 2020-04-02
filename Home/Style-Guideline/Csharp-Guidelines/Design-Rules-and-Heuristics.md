[[_TOC_]]

* Design coherent operations, that is, operations that fulfill only one task.

* Do without side effects: do not work with global variables and the like in your operations. Pass this kind of information as arguments, instead.

* A subclass should support all attributes, operations, and relations of its superclass; suppressions of these properties should be avoided.

* A subclass should not define constraints on inherited properties of its superclass.

* If inherited operations need to be overwritten, they should be compatible with the behavior of the overwritten ones.

* Aim for even distribution of knowledge about the application domain across all classes.

* Design your concepts to be as general as possible. That is, design with a view to interfaces instead of implementation.

* Design client-server relationships between classes (cooperation principal).

* Minimize dependencies between classes.

* The superclass of an abstract class is itself an abstract class too.

* Maximize the internal binding of classes. Responsibilities which belong together should be concentrated in one class.

* Minimize the external dependencies of a class. Keep the number of contracts (interfaces) with other classes to a minimum.

* Instead of functional modes, different operations should be provided. Where functional modes are used, use enum types as mode discriminators.

* Avoid indirect navigation. Limit the knowledge of classes about their neighboring classes.

* The code for one operation should not exceed one page. Lengthy operations are the hallmark of procedural programming. If an operation is lengthy, it is likely that it is a candidate for redesign.

* Mind uniform and descriptive names, data types, and parameter orders.

* If in an operation you find `switch/case` instructions or several consecutive instructions, this is a symptom of procedural thinking (polymorphism phobia).

* Take extreme values into account (minimum, maximum, nil, nonsense) and plan a robust behavior in all situations.

* Try to do without artificial or arbitrary limits (for example, a list with 14 entries) and try to implement dynamic behavior.

* It is never too early to start thinking about undo functions, user-specific configurations, user access right concepts, error handling, etc.

* Take company-specific and general standards into account.

* Avoid data-heavy and data-driven design. Behavior driven design has advantages over purely data-driven design. In data driven design, few central control classes emerge, but a high overall coupling of classes. In behavior-driven design the tasks are more equally divided across the classes, significantly fewer messages are generated, and the classes are coupled more loosely.

# Providing Access to Instance and Class Variables

Don't make any instance or class variables `public` or `protected` without good reason. Often, instance variables don't need to be explicitly set or gotten. Use a public or protected property instead. 

One example of appropriate public instance variables is the case where the class is essentially a data structure, with no behavior. In other words, if you would have used a `struct` instead of a class, then it's appropriate to make the class's instance variables public.

Use the `this` keyword when referencing instance fields in methods. The reader will be able to immediately differentiate between variables scoped to the method and those scoped to the object.

# Literals

Numerical constants (literals) should not be coded directly, except for -1, 0, and 1, which can appear in a `for` loop as counter values.

# Variable Assignments

Avoid assigning several variables to the same value in a single statement. It is hard to read.

Example: `fooBar.fChar = barFoo.lchar = 'c'; // AVOID!`

Do not use embedded assignments in an attempt to improve run-time performance. This is the job of the compiler. 

Example: `d = (a = b + c) + r; // AVOID!`

should be written as:

```
a = b + c;
d = a + r;
```

# Parentheses

It is generally a good idea to use parentheses liberally in expressions involving mixed operators to avoid operator precedence problems. Even if the operator precedence seems clear to you, it might not be to others-you shouldn't assume that other programmers know precedence as well as you do.

```
if (a == b && c == d) // AVOID!
if ((a == b) && (c == d)) // RIGHT
```

# Parameters

Check for valid parameter arguments. Perform argument validation for every public or protected method and property set accessor. Throw meaningful exceptions to the developer for invalid parameter arguments. Use the `System.ArgumentException` Class, or a class derived from `System.Exception`.

Constructor parameters used to initialize instance fields should have the same name as the instance field. 

Example:
```
public class Foo
{
    private string fooId;

    public foo(string fooId)
    {
        this.fooId = fooId;
    }
}
```

# Returning Values

Try to make the structure of your program match the intent. Example:

```
if (booleanExpression) 
{
    return true;
}
else
{
    return false;
}
```

should instead be written as: `return booleanExpression;`

Similarly,

```
if (condition)
{
    return x;
}
return y;
```

should be written as: `return condition ? x : y;`

# Avoid excessive nesting using guard clause

Just as indentation increasing the readability of code, it also contributes to ambiguity. Nesting happens when one control structure exists within another control structure, and possibly even another control structure. When reading code that resides within many nested blocks, the programmer must maintain an awareness of the pre-conditions that lead to the code being executed. Although a compiler is especially gifted at maintaining a stack of unresolved control structures, programmers are less so. Nesting becomes increasingly more ambiguous near the end of the control structures where for example code can be executed at the conclusion of an `if` block and prior to the conclusion of another `if` block.

```
public SomeMethod()
{
    for (int i = 1, i < 100, i++)
    {
        if (i > 10)
        {
            ... // Do something
            if (arg == someNumber)
            {
                ... // Do more
            }
        }
    }
}
```

Nesting becomes even more unreadable when code inside the structure stretches on for many lines or, in extreme situations, up to a page. Using the complement of the conditional expression leads to an early resolution of control structures and a flattening of the nesting.

`if (i > 10)` becomes: `if (i <= 10)`

A `continue` would be executed in order to start back at the top of the for block. This achieves a flattening of the nests, and a conditional block is resolved as quickly as possible.

```
public SomeMethod()
{
    for (int i = 1, i < 100, i++)
    {
        // Guard
        if (i <= 10)
        {
            continue;
        }
            ... // Do something
        if (arg == someNumber)
        {
            ... // do more
        }
    }
}
```

# Debug Code

Debug code should not be stripped from the source base. If debug code significantly contributes to the understanding and the maintenance of the code, then leave the debug code inside the class definition. The compiler will strip the debug code from the DLL's when a class is compiled for production.