# Localization
All of Adliance projects use Localization with .NET Resource files.
Most useful information is documented by Microsoft https://learn.microsoft.com/en-us/dotnet/core/extensions/localization

## Localization arguments

```csharp
LocalizedString localizedString = _localizer["GreetingMessage", dateTime, dinnerPrice];
```

All arguments of a Localization resource shall be described in the comment section of the default resource file.

```xml
<?xml version="1.0" encoding="utf-8"?>
<root>
  <data name="DinnerPriceFormat" xml:space="preserve">
    <value>On {0} my dinner cost {1}.</value>
    <comment>0: DateTime of dinner; 1: Price of the dinner</comment>
  </data>
</root>
```

The comment is shown in Lingohub, which helps translators to know the context when translating.
