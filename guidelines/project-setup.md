# How to setup a project

## Setup the repository
- Create a `readme.md` and shortly describe the project with information how developers have to setup their local environment. 
  - What prerequisites are necessary?
  - How to build the projects
  - How to run the projects
  - Include the build pipeline status images 
- Use an editor config file //TODO Reference to Adliance `.editorconfig`
- Use a `.gitingore` file
- Create a `src` folder for source projects.
- Create a `test` folder for test projects
- Create a `docs` folder for documentation. Write documentation in markup.

The project structure would look like:
```
src/
├───Adliance.Project
test/
├───Adliance.Project.Tests
docs/
readme.md
.editorconfig
.gitignore
```

## Setup a .NET project

- Use the latest .NET Version
- Enable nullability
- Enable implicit usings
- Treat warnings as errors
- Generate documentation files in WebAPI projects

```xml
<Nullable>enable</Nullable>
<ImplicitUsings>enable</ImplicitUsings>
<TreatWarningsAsErrors>true</TreatWarningsAsErrors>
<GenerateDocumentationFile>true</GenerateDocumentationFile>
```

- Put a `readme.md` in your project root to document specifics for this project.

### Test projects
Use [xUnit](https://xunit.net) as test framework.

Recommended libraries
-  [FluentAssertions](https://fluentassertions.com)

#### Integration tests
https://learn.microsoft.com/en-us/aspnet/core/test/integration-tests?view=aspnetcore-7.0#aspnet-core-integration-tests

#### UI tests
- [Playwright](https://playwright.dev/dotnet)
