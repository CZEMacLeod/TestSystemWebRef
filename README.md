# TestSystemWebRef

## Initial Create / Setup

```shell
dotnet new install MSBuild.SDK.SystemWeb.Templates@4.0.107
dotnet new systemweb
dotnet new gitignore
dotnet new globaljson --sdk-version 10.0.301
```

Ensure that the required SDK is installed with `dotnet --list-sdks`

## Test Class

Add a class that references a type in the `System.Web` namespace (requiring the `System.Web` assembly reference.

```cs
namespace ExampleEmptyWebApplication
{
    public class TestClass
    {
        public void Test(System.Web.HttpApplication application) { }
    }
}
```

## Build

```powershell
$vs_path = vswhere -latest -property installationPath
$vs_version = [System.Version]::Parse($(vswhere -latest -property installationVersion))
$vs_tools_path = "$vs_path\MSBuild\Microsoft\VisualStudio\v$($vs_version.Major).0"
$web_applications_target_path = "$vs_tools_path\WebApplications\Microsoft.WebApplication.targets"
$env:WebApplicationsTargetPath=$web_applications_target_path

&dotnet.exe build
```

or

```shell
dotnet build -p:WebApplicationsTargetPath="C:\Program Files\Microsoft Visual Studio\18\Professional\MSBuild\Microsoft\VisualStudio\v18.0\WebApplications\Microsoft.WebApplication.targets"
```

or

```powershell
.\build.ps1
```

## Result

```shell
Restore complete (0.3s)
  TestSystemWebRef net48 succeeded (0.1s) → bin\TestSystemWebRef.dll

Build succeeded in 0.9s
```