[[_TOC_]]

C# provides a mechanism for developers to document their code using XML. In source code files, lines that begin with /// and that precede a user-defined type such as a class, delegate, or interface; a member such as a field, event, property, or method; or a namespace declaration can be processed as comments and placed in a file.

XML documentation is required for classes, delegates, interfaces, events, methods, and properties. Include XML documentation for fields that are not immediately obvious. 

The following sample provides a basic overview of a type that has been documented.

```
using System;
/// <summary>
/// Class level summary documentation goes here.
/// </summary>
/// <remarks>
/// Longer comments can be associated with a type or member
/// through the remarks tag.
/// </remarks>
public class SomeClass
{
    /// <summary>
    /// Store for the name property.
    /// </summary>
    private string name;
    /// <summary>
    /// Name property.
    /// </summary>
    /// <value>
    /// A value tag is used to describe the property value.
    /// </value>
    public string Name
    {
        get
        {
            if (this.name == null)
            {
                throw new Exception("Name is null");
            }
            return myName;
        }
    }
    /// <summary>
    /// The class constructor.
    /// </summary>
    public SomeClass()
    {
        // TODO: Add Constructor Logic here
    }
    /// <summary>
    /// Description for SomeMethod.
    /// </summary>
    /// <param name="s">Parameter description for s goes here.</param>
    /// <seealso cref="String">
    /// You can use the cref attribute on any tag to reference a type
    /// or member
    /// and the compiler will check that the reference exists.
    /// </seealso>
    public void SomeMethod(string s) { }

    /// <summary>
    /// Some other method.
    /// </summary>
    /// <returns>
    /// Return results are described through the returns tag.
    /// </returns>
    /// <seealso cref="SomeMethod(string)">
    /// Notice the use of the cref attribute to reference a specific
    /// method.
    /// </seealso>
    public int SomeOtherMethod()
    {
        return 0;
    }
    /// <summary>
    /// The entry point for the application.
    /// </summary>
    /// <param name="args">A list of command line arguments.</param>
    public static int Main(String[] args)
    {
        // TODO: Add code to start application here
        return 0;
    }
}
```

XML documentation starts with `///`. When you create a new project, the wizards put some starter `///` lines in for you. 

The processing of these comments has some restrictions:

* The documentation must be well-formed XML. If the XML is not well-formed, a warning is generated and the documentation file will contain a comment saying that an error was encountered.

* Developers are not free to create their own set of tags.

* There is a recommended set of tags.

* Some of the recommended tags have special meanings:

* The `<param>` tag is used to describe parameters. If used, the compiler will verify that the parameter exists and that all parameters are described in the documentation. If the verification failed, the compiler issues a warning.

* The `cref` attribute can be attached to any tag to provide a reference to a code element. The compiler will verify that this code element exists. If the verification failed, the compiler issues a warning. The compiler also respects any using statements when looking for a
type described in the `cref` attribute.

* The `<summary>` tag is used by IntelliSense inside Visual Studio to display additional information about a type or member.

If you need to give information about a class, interface, variable, or method that isn't appropriate for documentation, use an implementation block comment or single-line comment immediately *after* the declaration.

Document comments must not be positioned inside a method or constructor definition block, because C# associates documentation comments with the first declaration after the comment.

Here are the XML documentation tags available:

Tag | Notes
---|----
`<c>` | The `<c>` tag gives you a way to indicate that text within a description should be marked as code. Use `<code>` to indicate multiple lines as code.
`<code>` | The `<code>` tag gives you a way to indicate multiple lines as code. Use `<c>` to indicate that text within a description should be marked as code.
`<example>` | The `<example>` tag lets you specify an example of how to use a method or other library member. Commonly, this would involve use of the `<code>` tag.
`<exception>` | The `<exception>` tag lets you document an exception class. Compiler verifies syntax.
`<include>` | The `<include>` tag lets you refer to comments in another file that describe the types and members in your source code. This is an alternative to placing documentation comments directly in your source code file.<br><br>The `<include>` tag uses the XML XPath syntax. Refer to XPath documentation for ways to customize your `<include>` use.<br>Compiler verifies syntax.
`<list>` | The `<listheader>` block is used to define the heading row of either a table or definition list. When defining a table, you only need to supply an entry for term in the heading.<br><br>Each item in the list is specified with an `<item>` block. When creating a definition list, you will need to specify both term and text. However, for a table, bulleted list, or numbered list, you only need to supply an entry for text.<br><br> A list or table can have as many `<item>` blocks as needed.
`<para>` | The `<para>` tag is for use inside a tag, such as `<remarks>` or `<returns>`, and lets you add structure to the text.
`<param>` | The `<param>` tag should be used in the comment for a method declaration to describe one of the parameters for the method. Compiler verifies syntax.
`<paramref>` | The `<paramref>` tag gives you a way to indicate that a word is a parameter. The XML file can be processed to format this parameter in some distinct way. Compiler verifies syntax.
`<permission>` | The `<permission>` tag lets you document the access of a member. The `System.Security.PermissionSet` lets you specify access to a member.
`<remarks>` | The `<remarks>` tag is where you can specify overview information about a class or other type. `<summary>` is where you can describe the members of the type.
`<returns>` | The `<returns>` tag should be used in the comment for a method declaration to describe the return value.
`<see>` | The `<see>` tag lets you specify a link from within text. Use `<seealso>` to indicate text that you might want to appear in a See Also section. Compiler verifies syntax.
`<seealso>` | The `<seealso>` tag lets you specify the text that you might want to appear in a See Also section. Use `<see>` to specify a link from within text.
`<summary>` | The `<summary>` tag should be used to describe a member for a type. Use `<remarks>` to supply information about the type itself.
`<value>` | The `<value>` tag lets you describe a property. 