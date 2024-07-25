# Cancellation Tokens

This document summarizes the usages and recommendations of cancellation tokens.

When using cancellation tokens they must be handed down the execution path. Every async method that supports a cancellation token as a parameter should be provided with the token. E.g the HttpClient methods.

When executing CPU-bound operations the token must be checked in interval if a cancellation is requested.

## Server

### Web API

For Web APIs cancellation tokens should only be used for longer running GET actions like searches/complex queries.

POST/PUT/PATCH/DELETE endpoints should normally not be cancellable to avoid data loss.

The cancellation token can be added to any controller action as a parameter and handed down to the executing code.

Azure App Services do probably not forward the cancellation from the browser. This is a limitation that needs to be considered. Generally this is depending on the reverse proxy / load balancer. With Kestrel and YARP this is maybe different. Still it is most probably not very reliable as the environmental conditions are hard to control.

https://github.com/dotnet/aspnetcore/issues/20229#issuecomment-623289191
https://learn.microsoft.com/en-us/answers/questions/1722078/cancellation-token-signal-not-being-received-by-th

A workaround would be the usage of WebSockets.

### Background Service

When implementing a custom background service by implementing `Microsoft.Extensions.HostingBackgroundService` the `ExecuteAsync` method has a cancellation token as a parameter. This parameter should be handed down to the execution code the be able to stop a background service gracefully.

The host waits in case of a graceful shutdown for a defined period of time after triggering the cancellation or until the `ExecuteAsync` method finishes. Therefore it can be necessary to add a delay in the `ExecuteAsync` method depending on the cleanup procedure.

# EF

The EF query methods also have cancellation token support. It depends on the DB provider if queries can or will be canceled when triggering the token.

## Blazor WASM

The cancellation token should be also used in all Blazor Pages/Components. 
When a Blazor page is fetching data in the `OnInitializedAsync` method (long running) and in the meantime the user is navigating away from the page to another page, the `OnInitializedAsync` method still continues to its end which reduces performance and can lead to bugs/sideffects (e.g unexpected updates of Breadcrumbs/global Components).

To approach this issue cancellation tokens can be used.

A base component can be implemented that provides a cancellation token which can be used in an implementing component.
This cancellation token can then be handed down the method call hierarchy until reaching the HttpClient or other services which have cancellation token support.

Base class:

```csharp
using System;
using System.Threading;
using Microsoft.AspNetCore.Components;

namespace RdaWeb.Blazor.Components;

/// <summary>
/// The base class with disposable cancellation token.
/// </summary>
public abstract class ComponentWithCancellationTokenBase : ComponentBase, IDisposable
{
    private CancellationTokenSource? _cancellationTokenSource;

    protected CancellationToken ComponentCancellationToken =>
        (_cancellationTokenSource ??= new CancellationTokenSource()).Token;

    public virtual void Dispose()
    {
        if (_cancellationTokenSource == null)
        {
            return;
        }

        _cancellationTokenSource.Cancel();
        _cancellationTokenSource.Dispose();
        _cancellationTokenSource = null;
        GC.SuppressFinalize(this);
    }
}
```

Child component `OnInitializedAsync` lifecycle method:

```csharp
protected override async Task OnInitializedAsync()
{
    var data = await FetchDataAsync(ComponentCancellationToken);
    IsInitialized = true;
    UpdateNavigationMenuWithData(data);
    await base.OnInitializedAsync();
}
```

API Client (deeper down in the `FetchDataAsync` call hierarchy)
```csharp
public async Task GetAsync(string path, CancellationToken cancellationToken,
    params (string, object?)[] queryParams)
{
    var query = ConvertQueryParameters(queryParams);
    var response = await _client.GetAsync(BuildUrl(path, query), cancellationToken);
    await HandleHttpResponseStatusAsync(response, cancellationToken);
}
```

The cancellation token is cancelled automatically when the page/component is disposed during a navigation. This results in an OperationCanceledException if e.g. API calls are still ongoing. This exception is automatically handled and ignored in the Blazor lifecycle. Because of this exception the ```UpdateNavigationMenuWithData``` method is never executed when the cancellation is triggered before `FetchDataAsync` is finished. 