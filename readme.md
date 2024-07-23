```pwsh
mkdir enforce-style
cd enforce-style
dotnet new console
dotnet new editorconfig
dotnet new gitignore
dotnet new tool-manifest
dotnet tool run dotnet-csharpier . --check
echo '	Console.WriteLine("Hello, World!"); // tab on this line, .editorconfig configure to use spaces' > Program.cs
```

Add 

```xml
  <Target Name="PreBuild" BeforeTargets="PreBuildEvent">
    <Exec Command="dotnet tool run dotnet-csharpier . --check" />
  </Target>
```

to the `enforce_style.csproj`

```pwsh
dotnet build
```