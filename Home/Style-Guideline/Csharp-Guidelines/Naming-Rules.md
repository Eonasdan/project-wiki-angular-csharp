[[_TOC_]]

Naming rules make programs more understandable by making them easier to read. They can also give information about the function of the identifier, for example, whether it's a constant, package, or class, which can be helpful in understanding the code.

Perhaps one of the most influential aids to understanding the logical flow of an application is how the various elements of the application are named. A name should tell "what" rather than "how." By avoiding names that expose the underlying implementation, which can change, you preserve a layer of abstraction that simplifies the complexity. For example, you could use `GetNextOrder()` instead of `GetNextArrayElement()`.

A tenet of naming is that difficulty in selecting a proper name may indicate that you need to further analyze or define the purpose of an item. Make names long enough to be meaningful but short enough to avoid being wordy. Programmatically, a unique name serves only to differentiate one item from another. Expressive names function as an aid to the human reader; therefore, it makes sense to provide a name that the human reader can comprehend. However, be certain that the names chosen are in compliance with the applicable rules and standards.

Following are recommended naming techniques:

# Methods

* Names of methods should contain active verb forms and imperatives (DeleteOrder, OpenSocket). It is not necessary to include the noun name when the active verb refers directly to the containing class. 

Example:

```
Socket.OpenSocket(); // AVOID! No need to mention "Socket" in name
Socket.Open(); // PREFER
```

* Avoid elusive names that are open to subjective interpretation, such as `Analyze()` for a routine, or `xxK8` for a variable. Such names contribute to ambiguity more than abstraction.

* Use the verb-noun method for naming routines that perform some operation on a given object, such as `CalculateInvoiceTotal()`.

* In method overloading, all overloads should perform a similar function.

# Variables

* Do use any `_` (underscore) to name a private class variable such as `private ApplicationDbContext _applicationDbContext`.

* Do not use Hungarian notation for field names. Good names describe semantics, not type.

* Prepend computation qualifiers (avg, sum, min, max, index) to the beginning of a variable name where appropriate.

* Use customary opposite pairs in variable names, such as min/max, begin/end, and open/close.

* In object-oriented languages, it is redundant to include class names in the name of class properties, such as `Book.BookTitle`. Instead, use `Book.Title`.

* Collections should be named as the plural form of the singular objects that the collection contains. A collection of `Book` objects is named `Books`.

* Boolean variable names should contain `Is` or `is` which implies Yes/No or True/False values, such as `isFound`, or `isSuccess`. 

* Avoid using terms such as Flag when naming status variables, which differ from Boolean variables in that they may have more than two possible values. Instead of `orderFlag`, use a more descriptive name such as `orderStatus`.

* Even for a short-lived variable that may appear in only a few lines of code, still use a meaningful name. Use single-letter variable names, such as `i` or `j` for short-loop indexes only.

* Constants should not be all uppercase with underscores between words, such as `NUM_DAYS_IN_WEEK`. Constants follow the same naming rules as properties. The aforementioned constant would be named `NumDaysInWeek`.

* Temporary variables should always be used for one purpose only; otherwise, several variables should be declared.

# Parameters

* Do not prefix method parameters with any special character to indicate that they are parameters.

* Parameter names should follow the naming rules for variables (above).

# Tables
* When naming tables, express the name in the singular form. For example, use `Employee` instead of `Employees`.

* When naming columns of tables, do not repeat the table name; for example, avoid having a field called `EmployeeLastName` in a table called `Employee`.

* Do not incorporate the data type in the name of a column. This will reduce the amount of work needed should it become necessary to change the data type later.

* Column names should follow the same rules as properties e.g. `FirstName`.

# Microsoft SQL Server
* Do not prefix stored procedures with `sp_`, because this prefix is reserved for identifying system-stored procedures.
* In Transact-SQL, do not prefix variables with `@@`, which should be reserved for truly global variables such as `@@IDENTITY`.

# General
* Implementation details, in particular type specifications, should not be mention in the name of a descriptor. This is a common trait in procedural languages like Visual Basic where lowercase prefixes are used to encode the data type in the name of the identifier, such as `oInvoice`. This approach is not applicable to contemporary languages where the aforementioned identifier is written simply as `invoice`.

* Names with semantic content are preferred to names with type specifications (`sizeOfArray` instead of `anInteger`).

* Names of descriptors should be chosen in such a way that they can be read like a sentence within instructions.

* Minimize the use of abbreviations. If abbreviations are used, be consistent in their use. An abbreviation should have only one meaning and likewise, each abbreviated word should have only one abbreviation. For example, if using `min` to abbreviate `minimum`, do so everywhere and do not later use it to abbreviate `minute`.

* When naming methods, include a description of the value being returned, such as `GetCurrentCustomerName()`. 

* File and folder names, like method names, should accurately describe what purpose they serve.

* Avoid homonyms when naming elements to prevent confusion during code reviews, such as `write` and `right`.

* When naming elements, be aware of commonly misspelled words. Also, be aware of differences that exist between American and British English, such as color/colour and check/cheque.

# Spelling

It is recommended that you install [this spell checker plugin](https://marketplace.visualstudio.com/items?itemName=EWoodruff.VisualStudioSpellCheckerVS2017andLater).

* Do not short hand words. Always spell words out completely.

# Abbreviations

To avoid confusion and guarantee cross-language interoperation, follow these rules regarding the use of abbreviations:

* When using acronyms, use camel case for acronyms more than two characters long. For example, use `HtmlButton`. However, you should capitalize acronyms that consist of only two characters, such as `System.IO` instead of `System.Io`.

* Do not use abbreviations in identifiers or parameter names.

* Do not use abbreviations or contractions as parts of identifier names. For example, use `GetWindow` instead of `GetWin`.

* Do not use acronyms that are not generally accepted in the computing field. Where appropriate, use well-known acronyms to replace lengthy phrase names. For example, use `UI` for User Interface and `OLAP` for On-line Analytical Processing.

# Capitalization

Use the following three conventions for capitalizing identifiers:

## Pascal case
The first letter in the identifier and the first letter of each subsequent concatenated word are capitalized. You can use Pascal case for identifiers of three or more characters. For example: `BackColor`.

## Camel case
The first letter of an identifier is lowercase and the first letter of each subsequent concatenated word is capitalized. For example: `backColor`.

## Uppercase
All letters in the identifier are capitalized. Use this convention only for identifiers that consist of two or fewer letters. For example: `System.IO`, `System.Web.UI`.

You might also have to capitalize identifiers to maintain compatibility with existing, unmanaged symbol schemes, where all uppercase characters are often used for enumerations and constant values. In general, these symbols should not be visible outside of the assembly that uses them. 

The following table provides rules and example for common identifiers:

Identifier Type | Rules for Naming | Examples
----------------|------------------|---------
Namespaces | Namespace names should be nouns, in Pascal case. Avoid the use of underscores ("_") in namespace names. Try to keep names simple and descriptive. Use whole words and avoid acronyms and abbreviations unless the abbreviation is much more widely used than the long form, such as Url or Html. All custom namespace names are to begin with the company name if applicable, followed by the project, product, or technology name, and the purpose name, followed by the purpose of the package as an organizational unit. | `MyCompany.Framework.Data; MyCompany.Factories;` 
Classes | Class names should be nouns, in Pascal case. As with namespaces, keep class names simple and descriptive. Use whole words and avoid acronyms and abbreviations unless the abbreviation is much more widely used than the long form, such as Url or Html. | `class SalesOrder; class LineItem; class HtmlWigets;`
Interfaces | Interface names use Pascal case and begin with the letter "I". | `interface IBusinessRule;`
Methods | Methods should be active verb/nouns forms, in Pascal case. `GetDataRow(); UpdateOrder();`
Instance Fields | Instance fields are in camel case. Variable names should not start with underscore, even though it is allowed.<br/><br/>Variable names should be meaningful. The choice of a variable name should be mnemonic – that is, designed to indicate to the casual observer the intent of its use. One-character variable names should be avoided. | `protected string name; private int orderId; private string lastName; private float width; // AVOID! private _total;`
Enum Types and Enum Values | Enum types and values are in Pascal case. Use abbreviations sparingly. Do not use an Enum suffix on Enum type names. Use a singular name for most Enum types, but use a plural name for Enum types that are bit fields. | `enum Status {ReadyToGo,  WaitingForNow}; enum Day {Monday, Tuesday};`
Events | Events are in Pascal case. Use the suffix `EventHandler` on event handler names. Specify two parameters named `sender` and `e`. The sender parameter represents the object that raised the event. The sender parameter is always of type `object`, even if it is possible to use a more specific type. The state associated with the event is encapsulated in an instance of an event class named `e`. Use an appropriate and specific event class for the e parameter type. Name an event argument class with the `EventArgs` suffix. Consider naming events with a verb. Use a gerund (the "ing" form of a verb) to create an event name that expresses the concept of pre-event, and a past-tense verb to represent post-event. For example, a `Close` event that can be canceled should have a `Closing` event and a `Closed` event. Do not use the `BeforeXxx/AfterXxx` naming pattern. Do not use a prefix or suffix on the event declaration on the type. For example, use `Close` instead of `OnClose`. In general, you should provide a protected method called `OnXxx` on types with events that can be overridden in a derived class. This method should only have the event parameter `e`, because the sender is always the instance of the type. |  `public delegate voidMouseEventHandler(object sender, MouseEventArgs e);`
Exception Classes | Exception classes are in Pascal case and always have the suffix `Exception`. | `InvalidCastException DomainValueException`
Custom Attributes |Custom attributes are in Pascal case and always have the suffix `Attribute`. `PersistentEntityAttribute`
Properties | Properties are in Pascal case with an. Property names should directly reflect the underlying attribute. `public int OrderId public string LastName`
Object References | Objects references are camel case when non-public and pascal case when public (although references should never be public without good reason). Except where exceptionally warranted, objects are named after their class. An exception to this rule would be when two or more objects are needed of the same class within the same scope. Avoid naming object references as abbreviations or acronyms of the class name. | `public string Name; Order order = new Order; LineItem lineItem = new LineItem();`
Constants | Constants are in Pascal case. They should not be all uppercase with words separated by underscores (`_`). | `const int NumDaysInWeek = 4;`<br/>`const int NUM_DAYS_IN_WEEK = 4; // AVOID! `