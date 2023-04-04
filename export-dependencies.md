# I added a dependency to my project via NuGet (e.g. NAudio) or via manual import (like a lib from another plugin creator), but it's not copying its DLL to the output folder when I build the project to test or when I send it to Plogon Build.

To fix this, you need to configure your project to output the dependencies. Thankfully, it's just one line!

Open the project's `.csproj` file and add this line to a `<PropertyGroup>` block (usually the one with parameters like `<TargetFramework>`):

```xml
        <CopyLocalLockFileAssemblies>true</CopyLocalLockFileAssemblies>
```

Example of it inside a `<PropertyGroup>`:

```xml
    <PropertyGroup>
        <TargetFramework>net7.0-windows</TargetFramework>
        <Platforms>x64</Platforms>
        <Nullable>enable</Nullable>
        <LangVersion>latest</LangVersion>
        <AllowUnsafeBlocks>true</AllowUnsafeBlocks>
        <ProduceReferenceAssembly>false</ProduceReferenceAssembly>
        <AppendTargetFrameworkToOutputPath>false</AppendTargetFrameworkToOutputPath>
        <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
        <!-- adds dependencies (in this case, NAudio) to the output folder-->
        <CopyLocalLockFileAssemblies>true</CopyLocalLockFileAssemblies>
    </PropertyGroup>
```

It should then output the DLLs of the dependencies to the output folder.
