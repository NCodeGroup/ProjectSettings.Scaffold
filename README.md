[buildCrossTargeting]: https://github.com/Microsoft/msbuild/issues/1860
[SPDX license]: https://github.com/NuGet/Home/wiki/Packaging-License-within-the-nupkg-(Technical-Spec)#license-expression-pack
[NU5048]: https://aka.ms/deprecateIconUrl

# Overview

[![Build status](https://ci.appveyor.com/api/projects/status/fwoj34tnk343gg4e/branch/master?svg=true)](https://ci.appveyor.com/project/polewskm/ncode-projectsettings-scaffold/branch/master)

Contains common settings, scripts, and files to scaffold C# projects for NCodeGroup.

## Release Notes

* v1.0.0 - Initial release
* v1.0.1 - Added support for multi-targeting projects (see [buildCrossTargeting])
* v1.0.2 - Packing of additional files
* v1.0.3 - Updating MSBuild properties
* v1.0.4 - Added additional examples to project.props
* v1.0.5 - Updates for NET Core SDK
* v1.0.6 - Updates for [SPDX license] expression
* v1.0.7 - Change default for CLS compliance to False
* v1.0.8 - Added `Directory.Build.props`
* v1.0.9 - Deprecating `PackageIconUrl` in favor of `PackageIcon` (see [NU5048])
* v1.0.10 - Pack README and added option for default branch name (used in NuGet package icon)
* v1.0.11 - Added setting for ContinuousIntegrationBuild