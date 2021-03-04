---
title: gRPC on .NET supported platforms
author: jamesnk
description: Learn about the supported platforms for gRPC on .NET.
monikerRange: '>= aspnetcore-3.0'
ms.author: jamesnk
ms.date: 01/22/2021
no-loc: [appsettings.json, "ASP.NET Core Identity", cookie, Cookie, Blazor, "Blazor Server", "Blazor WebAssembly", "Identity", "Let's Encrypt", Razor, SignalR]
uid: grpc/supported-platforms
---
# gRPC on .NET supported platforms

By [James Newton-King](https://twitter.com/jamesnk)

This article discusses the requirements and supported platforms for using gRPC with .NET. There are different requirements for the two major gRPC workloads:

* Hosting gRPC services on the server.
* Calling gRPC services from a client.

gRPC takes advantage of advanced features available in HTTP/2. HTTP/2 isn't supported everywhere, but a second wire-format using HTTP/1.1 is available for gRPC:

* [`application/grpc`](https://github.com/grpc/grpc/blob/master/doc/PROTOCOL-HTTP2.md) - gRPC over HTTP/2 is how gRPC is typically used.
* [`application/grpc-web`](https://github.com/grpc/grpc/blob/master/doc/PROTOCOL-WEB.md) - gRPC-Web modifies the gRPC protocol to be compatible with HTTP/1.1. gRPC-Web can be used in more places. gRPC-Web can be used by browser apps and in networks without complete support for HTTP/2. Two advanced gRPC features are no longer supported: client streaming and bidirectional streaming.

gRPC on .NET supports both wire-formats. `application/grpc` is used by default. For information on setting up gRPC-Web, see <xref:grpc/browser>.

## ASP.NET Core gRPC server requirements

Hosting gRPC services with ASP.NET Core requires .NET Core 3.x or later.

> [!div class="checklist"]
>
> * .NET 5 or later
> * .NET Core 3

ASP.NET Core gRPC services can be hosted on all operating system that .NET Core supports.

> [!div class="checklist"]
>
> * Windows
> * Linux
> * macOS&dagger;

&dagger;[macOS doesn't support hosting ASP.NET Core apps with HTTPS](xref:grpc/troubleshoot#unable-to-start-aspnet-core-grpc-app-on-macos).

### Supported ASP.NET Core servers

All built-in ASP.NET Core servers are supported.

> [!div class="checklist"]
>
> * Kestrel
> * TestServer
> * IIS&dagger;
> * HTTP.sys&Dagger;

&dagger;IIS requires .NET 5 and Windows 10 Build 20241 or later.

&Dagger;HTTP.sys requires .NET 5 and Windows 10 Build 19529 or later.

For information about configuring ASP.NET Core servers to run gRPC, see <xref:grpc/aspnetcore#server-options>.

### Azure services

> [!div class="checklist"]
>
> * [Azure Kubernetes Service (AKS)](https://azure.microsoft.com/services/kubernetes-service/)
> * [Azure App Service](https://azure.microsoft.com/services/app-service/)&dagger;

&dagger;Azure App Service doesn't support hosting gRPC over HTTP/2. gRPC-Web is a compatible alternative.

Work is in-progress to improve support for gRPC with HTTP/2 in Azure App Service. For more information, see [this GitHub issue](https://github.com/dotnet/AspNetCore/issues/9020).

## .NET gRPC client requirements

The [Grpc.Net.Client](https://www.nuget.org/packages/Grpc.Net.Client/) package supports gRPC over HTTP/2 on .NET Core 3 and .NET 5 or later.

Limited support is available for gRPC over HTTP/2 on .NET Framework. Other .NET versions such as UWP, Xamarin and Unity don't have required HTTP/2 support, and must use gRPC-Web instead.

> [!div class="checklist"]
>
> * .NET 5 or later
> * .NET Core 3
> * .NET Framework&dagger;
> * .NET Standard 2.0 (including UWP, Xamarin, Unity)&Dagger;
> * Blazor WebAssembly&Dagger;

&dagger;.NET Framework requires <xref:System.Net.Http.WinHttpHandler> to be configured and Windows 10 Build 19622 or later.

&Dagger;Blazor WebAssembly and .NET Standard 2.0 can call gRPC services with gRPC-Web.

Using `Grpc.Net.Client` on .NET implementations other than .NET Core or .NET 5 requires additional configuration. For more information, see <xref:grpc/netstandard>.

## Additional resources

* <xref:grpc/netstandard>
* [gRPC C# core-library](https://grpc.io/docs/languages/csharp/quickstart/)
