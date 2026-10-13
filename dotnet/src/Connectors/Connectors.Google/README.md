# Community Semantic Kernel Google Connectors

This is an **unofficial fork**, not a Microsoft or Google release. It is based on
`Microsoft.SemanticKernel.Connectors.Google` version `1.81.0-alpha` from the
upstream `dotnet-1.81.0` tag.

## Patch

Gemini function-response messages serialize with `role: "user"` instead of the
unsupported `role: "function"`. Internal Semantic Kernel tool roles,
`functionResponse` payloads, and thought signatures are preserved.

This patch addresses the rejected tool-result continuation request. It does not
change empty-response handling or retry behavior.

## Installation

Replace your reference to `Microsoft.SemanticKernel.Connectors.Google` with:

```xml
<PackageReference Include="Community.SemanticKernel.Connectors.Google" Version="1.81.0-alpha.1" />
```

Do not install both Google connector packages together: they contain the same
`Microsoft.SemanticKernel.Connectors.Google` assembly. Existing namespaces and
connector APIs are unchanged. Continue using the official Semantic Kernel core
and abstractions packages at compatible `1.81.0` versions.

The package targets .NET 10, .NET 8, and .NET Standard 2.0.

## Building the package

From the repository's `dotnet` directory:

```powershell
dotnet pack src\Connectors\Connectors.Google\Connectors.Google.csproj -c Publish -o .\artifacts\nuget
```

The `Publish` configuration compiles against the official, signed Semantic Kernel
`1.81.0` packages. Other configurations retain upstream project references for
development and tests. Use `Publish` for distribution: locally built unsigned
core assemblies are not interchangeable with the official NuGet assemblies.

This packs the connector only. Inspect its metadata and dependencies before
publication, and publish only the `Community.SemanticKernel.Connectors.Google`
package, not the upstream core or abstractions packages. Commit the source changes
and rebuild before publication so the package's repository commit identifies the
packaged source.

## Source and license

- Fork: https://github.com/lil-kita/semantic-kernel-google-connector
- Upstream: https://github.com/microsoft/semantic-kernel

Distributed under the upstream MIT license. Microsoft copyright notices and the
repository's license remain intact.
