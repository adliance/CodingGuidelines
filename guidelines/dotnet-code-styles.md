# Design guidelines
Adliance uses the defined .NET design guidelines from Microsoft https://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/

There you find very important guidelines, which are mandatory to know:
- Naming
- Type design
- Member design
- Exception design
- Usages of framework functionality

# Code styles
Adliance tries to have a consistent code base of the common code styles by using [EditorConfig](https://editorconfig.org/) files.

Settings in EditorConfig files let you maintain consistent coding styles and settings in a codebase, such as indent style, tab width, end of line characters, encoding, and more, regardless of the editor or IDE you use.

These [Code styles](https://github.com/adliance/Buddy/tree/master/src/Adliance.Buddy.CodeStyle) are distributed through a [nuget package](https://www.nuget.org/packages/Adliance.Buddy.CodeStyle) which can be included on solution level.
The developers EditorConfig-compliant IDE should consider and suggest those rules. 

## Format code
Despite having your IDE formatting the code, you can always format your code with the [dotnet format](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-format) tool. The tool uses your `.editorconfig` files and brings your files to a correct format.

# Common rules
- Use interfaces when using collections, according to "Always implement to an interface not an implementation".
- Use statement expression when statement body is only one line.
- [Async Naming convention](https://learn.microsoft.com/en-us/dotnet/csharp/asynchronous-programming/task-asynchronous-programming-model#BKMK_NamingConvention)
- Tuples as parameters or return types of public methods
  - Favor classes over tuples
  - Only used named tuples
- `if` statements should handle errors first
- Avoid nested if statements due to readability

## Commenting guidelines
- Public members should have XML comments
- Especially API actions must have good XML comments, which describe the functionality, query parameters and status codes in a good detail. This is very important for the Swagger documentary generated from it.

# Razor
- Always create a [Code-Behind](https://learn.microsoft.com/en-us/aspnet/core/blazor/components/?view=aspnetcore-7.0#partial-class-support) file (`.razor.cs`) for a Razor component.
- Parameters (properties with `[Parameter]`` attribute) must always have an XML comment as a description. So that the user of the component knows what to pass and what the effects of the property are.
- Please always start non-string properties with `@`. This increases the readability of the used variable or data type. E.g. `<TelerikWindow Modal="@true">`. [See Microsoft Guideline](https://learn.microsoft.com/en-us/aspnet/core/blazor/components/?view=aspnetcore-7.0#markup)

# Entity Framework
- Use entity configurations

# Web API
- API project guidelines,
- naming of routes,
- Swagger documentation
- models,
- project structure

# MVC

