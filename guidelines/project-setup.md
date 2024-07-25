# How to setup a project

## Setup the repository
- Create a `readme.md` and shortly describe the project with information how developers have to setup their local environment. 
  - What prerequisites are necessary?
  - How to build the projects
  - How to run the projects
  - Include the build pipeline status images 
- Use an editor config file //TODO Reference to Adliance `.editorconfig`
- Use a `.gitignore` file
- Create a `src` folder for source projects.
- Create a `test` folder for test projects
- Create a `docs` folder for documentation. Write documentation in markup.

The project structure would look like:
```
src/
├── Adliance.Project
test/
├── Adliance.Project.Tests
docs/
readme.md
.editorconfig
.gitignore
```

### Configure Azure DevOps Pull Request checklists

A pull request template is a file containing Markdown text that populates the PR description when you create a PR. Good PR descriptions tell PR reviewers what to expect, and can help track tasks like adding unit tests and updating documentation.

Use the [.azuredevops](../.azuredevops) folder in this repository as a template.

More information see [Pull Request templates](https://learn.microsoft.com/en-us/azure/devops/repos/git/pull-request-templates?view=azure-devops).

## Setup a .NET project

- Use the latest .NET Version
- Enable nullability
- Enable implicit usings
- Generate documentation files in WebAPI projects
- Add Adliance.Buddy.CodeStyle

```xml
<Nullable>enable</Nullable>
<ImplicitUsings>enable</ImplicitUsings>
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
