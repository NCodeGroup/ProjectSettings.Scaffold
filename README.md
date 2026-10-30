# Deprecated

> **This package is retired. Use [NCodeGroup/project-template](https://github.com/NCodeGroup/project-template), which replaces it.**
>
> - It shipped shared MSBuild settings, `.editorconfig`, `.gitattributes`, code-style rules, `Directory.Build.props` and Copilot instructions into a project. The template does the same job, and also gives a project CI, Dependabot, central package management and the agent workflow, and keeps it current with template updates.
> - To move a library off this package, run `Adopt-Project.ps1 -Path <the repository>` from a clone of the template. It removes the `NCode.ProjectSettings.Scaffold` reference, moves the package versions into `Directory.Packages.props`, and takes the build settings from `build/ProjectTemplate.props`.
> - Already moved: Buffers, Base64Url, Collections.Providers, Mediator, NCode.Disposables, PropertyBag and Extensions.DataProtection.
>
> The NuGet package `NCode.ProjectSettings.Scaffold` is deprecated and this repository is archived. The code stays available as it is.

[buildCrossTargeting]: https://github.com/Microsoft/msbuild/issues/1860
[SPDX license]: https://github.com/NuGet/Home/wiki/Packaging-License-within-the-nupkg-(Technical-Spec)#license-expression-pack
[NU5048]: https://aka.ms/deprecateIconUrl

# Overview

[![ci](https://github.com/NCodeGroup/ProjectSettings.Scaffold/actions/workflows/main.yml/badge.svg)](https://github.com/NCodeGroup/ProjectSettings.Scaffold/actions)

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
* v1.0.12 - Removed setting for PackageProjectUrl
* v1.0.13 - Moving CI build from appveyor to github actions
* v1.0.14 - LF line endings and copilot settings
* v1.0.15 - Fix nuspec wildcard handling
* v1.0.16 - Fix targets wildcard handling
* v1.0.17 - Remove deprecated iconUrl
* v1.0.18 - Remove PackageIconUrl msbuild property
* v1.0.19 - Fix gitattributes for images
* v1.0.20 - Disable XML doc for test projects
* v1.0.21 - Added C# code style settings for parameter/argument wrapping and attribute placement
