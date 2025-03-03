# 5.0.1

- Added support for additional files on `GetWorkspace()` (#231, thanks @Corniel).

# 5.0.0

- Updating Buildalyzer to target .NET 6 (#221, thanks @colombod).

# 4.1.7

- Updated `Microsoft.CodeAnalysis.CSharp.Workspaces` and `Microsoft.CodeAnalysis.VisualBasic.Workspaces` to 4.4.0 (#220, thanks @colombod).

# 4.1.6

- Fixed a `NullReferenceException` for F# projects (#216, thanks @psfinaki).

# 4.1.5

- Added a `BuildEnvironment.NoAutoResponse` option to control whether the `/noAutoResponse` argument is set, with a default of `true` to avoid processing `.rsp` files that could conflict with Buildalyzer (#211).
- Add API to retrieve compiler command-line and arguments (#212, #213, thanks @siegfriedpammer).

# 4.1.4

- Added support for Visual Basic projects (#207, thanks @cslong).
- Added support for the `additionalfile` compiler argument as `IAnalyzerResult.AdditionalFiles` (#200). 

# 4.1.3

- Ensured all project references are distinct (#203, #204, thanks @Mingxue008, @Therzok, and @slang25).

# 4.1.2

- Updated `MsBuildPipeLogger` to 1.1.6.
- Updated `Microsoft.CodeAnalysis` to 4.1.0.

# 4.1.1

- Added SourceLink support.

# 4.1.0

- Updated `Buildalyzer.Logger` to target .NET Standard 2.0.
- Updated `MsBuildPipeLogger` references to version 1.1.4.

# 4.0.0

- Updated Buildalyzer to target .NET Core 3.1 (#197, #189, thanks @AdaskoTheBeAsT and @slang25).
- Made `AnalyzerResults.TargetFrameworks` and related properties deterministically ordered (#198, thanks @0xced).

# 3.2.9

- Added additional logging for Roslyn workspace creation in `Buildalyzer.Workspaces`.

# 3.2.8

- Reverted `UseAppHost` back to defaults for Buildalyzer builds in favor of setting `ComputeNETCoreBuildOutputFiles` instead so that self-contained application builds still work (#194, #185, #187).
- Added ability to bypass MSBuild when using .NET Core/.NET (I.e. the `dotnet` command) so that other commands like `publish` can be invoked (#195, thanks @echalone).
- Added support for analyzing build logs that don't set a `TargetFrameworkMonitor` (I.e. C++ projects) (#196, thanks @echalone).

# 3.2.7

- Fixed MSBuild polling in Visual Studio directories when Visual Studio 2022 is installed since it now installs into the normal "Program Files" folder (as opposed to the x86 one).

# 3.2.6

- Specifies an encoding for source text in `Buildalyzer.Workspaces` to avoid CS8055 errors ("Cannot emit debug information for a source text without encoding") when compiling the workspace (#128).

# 3.2.5

- Added a strongly-typed `PreprocessorSymbols` collection to `AnalyzerResults` and used it to flow constants through to `Buildalyzer.Workspaces` for .NET 5 and up projects (#191, #192, thanks @richardwerkman).
- Set `UseAppHost` to false for Buildalyzer builds since there's no need to create native executables for analysis (#185, #187, thanks @slang25).
- Added a test project for checking .NET 6 compatibility (#185, #186, thanks @bernd5).

# 3.2.4

- Updated structured logging library to consolidate MSBuild and binary logging types (internal change, should be no impact to consumers).

# 3.2.3

- Fixed a bug where Buildalyzer.Workspaces would not add transitive references to projects in the Roslyn workspace (#181).
- No longer attempts to add F# projects from a solution to the Roslyn workspace in Buildalyzer.Workspaces which causes an exception in Roslyn.
- Updated structure logging support to the latest package providing binlog version 14 parsing (#184).
- Updated Microsoft.CodeAnalysis package references in Buildalyzer.Workspaces to 3.11.0.
- Updated MSBuild libraries for programmatic use by Buildalyzer to 16.10.0.

# 3.2.2

- Fixed a bug with WPF custom control libraries (#178, #179, thanks @markrendle)

# 3.2.1

- Sets SolutionFilePath in the Workspace Solution when it's available (#177, thanks @markrendle)
- Fixed `ProjectAnalyzer` exceptions when the solution file is not in the source root (#175, #176, thanks @psfinaki)
- Fixed a small QOL change needed when using Buildalyzer for F# (#172, thanks @dukedagmor)
- Fixed bug when `PackageReference` contains the name of a package in `Update` instead of `Include` (#170, #171, thanks @eNeRGy164)
- Refactored Buildalyzer.Workspaces so a Microsoft.CodeAnalysis.VisualBasic.Workspaces reference is not needed when not using Visual Basic features (#168, #169, thanks @svick)

# 3.2.0

- Refactored `ProjectItem` to an interface `IProjectItem` for easier mocking/testing (#161, #162, thanks @fbd)
- Fixed .NET Framework TFM identification for .NET Core/.NET 5 and others (#163, #164, thanks @slang25)
- Automatically adds project references that didn't originally exist in the manager when building a Roslyn workspace (#159, #160, thanks @slang25)

# 3.1.1

- Added Workspaces support for analyzers and source generators (#157, #158, thanks @svick)
- Updated the Microsoft.CodeAnalysis packages to 3.8.0 (#155, thanks @jjonescz)
- Added a fix for F# support (#151, #152, thanks @dukedagmor)

# 3.1.0

- Added `SourceFiles` and `References` for F# projects (#146, thanks @dukedagmor)
- Fixed an inconsistency between Buildalyzer and MSBuild by adding a trailing directory separator to the solution path (#147, #148, thanks @laurenceSaes)

# 3.0.1

- Fixed (hopefully) several bugs related to concurrency (#142, #134, #138, thanks @duncanawoods and @SierraNL).

# 3.0.0

- Added support for specifying additional MSBuild arguments via `EnvironmentOptions.Arguments`.
- Updated the MSBuild.StructuredLogger package to version 2.1.133
- Updated MSBuild packages to 16.5.0 (#140, thanks @colombod)
- Updated Microsoft.CodeAnalysis packages to 3.6.0
- The result of these package updates is that while Buildalyzer itself targets .NET Standard 2.0, any consuming application will need to target either .NET Core 2.1 or .NET Framework 4.7.2 (or higher)

# 2.6.0

- [Refactoring] Refactored key classes into interfaces for easier testing (#132, thanks @richardwerkman)

# 2.5.1

- [Fix] Removed the explicit encoding parameter when generating a `SourceText` in Buildalyzer.Workspaces (#128)
- [Fix] Fixes a race condition in `ProcessRunner` in `Process.WaitForExit()` calls (#125, thanks @duncanawoods)

# 2.5.0

- [Fix] Fix for finding the default SDK in some scenarios due to differences in output from dotnet (#120, thanks @patriksvensson)
- [Refactoring] Updates `Microsoft.CodeAnalysis` dependencies in `Buildalyzer.Workspaces` (#124, thanks @farnyser)
- [Feature] Support for F# projects (#123)

# 2.4.0

- [Fix] Removes `IProjectTransformer` since Buildalyzer no longer feeds project files to the MSBuild API (#114)
- [Feature] Adds back project filtering (#118)
- [Fix] Added "System.Reflection.TypeExtensions" as a direct dependency for .NET Framework consumers (#116)
- [Fix] Disable the COREHOST_TRACE environment variable (#115, thanks @sapsari)

# 2.3.0

- [Feature] Package references are now available directly in `ProjectFile` (#111, thanks @eNeRGy164)
- [Feature] Better future-proof MSBuild path discovery (#106, thanks @colombod)
- [Fix] Fixes for csc arguments parser (#100, thanks azyobuzin)

# 2.2.0

- [Fix] Several fixes for parsing the `csc` command line arguments from the build log (#89)
- [Feature] Passes all defined constants from the build to Roslyn (#86)
- [Feature] Now uses a single MSBuild submission and defers restore phase to MSBuild (#66)
- [Feature] Better processing of `dotnet` console output (#94, thanks @jonstelly)
- [Feature] Better support for two-phase builds like Razor projects (#92, #93, thanks @jonstelly)
- [Feature] Parallelize project builds when creating a Roslyn workspace (#91, thanks @jonstelly)
- [Refactoring] Scopes project ID cache when creating Roslyn workspaces to `AnalyzerManager` (#87. #88, thanks @wadinj)
- [Feature] Adds support for setting a custom `dotnet.exe` path (#84, thanks @itn3000)
- [Fix] Avoid exceptions when overwriting existing keys in `EnvironmentOptions` (#83, thanks @itn3000)
- [Feature] Adds `AnalyzerResult.PackageReferences` to easily access project package references (#82, thanks @mholo65)

# 2.1.0

- [Feature] Adds `AnalyzerManager.Analyze()` support for reading MSBuild binary log files
- [Fix] Fix for pipe communication problems on Linux

# 2.0.1

- [Fix] Fix for hang when the MSBuild process fails to start or logger doesn't connect (#78)

# 2.0.0

- **[Breaking Change]** [Refactoring] Entire API...again. Consider this the "if at first you don't succeed" release.
- [Refactoring] Now uses MSBuild directly by launching out-of-process MSBuild instances instead of the API - if you can build it, Buildalyzer should be able to
- [Refactoring] Reduced build methods to just `ProjectAnalyzer.Build()` and overloads - every build builds now builds every target framework unless otherwise specified and always returns an `AnalyzerResults`
- [Refactoring] `AnalyzerResult` build results are now limited to what we can pull out of MSBuild logs (which is surprisingly a lot) - file an issue if you're missing something you used to get from the old MSBuild API results

# 1.0.1

- [Fix] Fix for AssemblyInfo BOM marking (#74, thanks @bhugot)
- [Refactoring] Updated MSBuild assemblies
- [Refactoring] Updated logging assemblies (#69, thanks @ltcmelo)
- [Fix] Fixes for cross-platform path handling (#67, #68, thanks @ltcmelo)

# 1.0.0

- **[Breaking Change]** [Refactoring] Entire API. Most of the concepts are the same, but the API has changed significantly since the last release (too many changes to enumerate). Documentation is forthcoming, but I wanted to get this release out the door as soon as possible.
- [Refactoring] Introduces a `ProjectTransformer` base class for specifying project file adjustments instead of a delegate
- [Fix] Converts multi-targeted projects into a single target so Buildalyzer can build them (#29, #57)
- [Fix] Calling `ProjectAnalyzer.SetGlobalProperty` and `ProjectAnalyzer.RemoveGlobalProperty` no longer leaks to projects sharing the same `BuildManager`
- [Feature] Added ability to set global properties at the `AnalyzerManager` level (#52, thanks @dfederm)
- [Feature] Added ability to set environment variables for `AnalyzerManager` (all projects) and `ProjectAnalyzer` (specific project)

# 0.5.0

- [Fix] Updated MSBuild API references for latest Visual Studio and .NET SDKs
- [Fix] Added `DisableRarCache` MSBuild property and set to `false` (#56)
- [Fix] Added `NuGet.Common` and `NuGet.ProjectModel` since they're no longer shipped in the box with the .NET SDK (#49, #54)

# 0.4.0

- [Fix] Updated MSBuild API references for latest Visual Studio and .NET SDKs
- [Refactoring] Internally refactored the way temporary environment variables are set and unset
- [Feature] Sets environment variable MSBUILD_EXE_PATH while preserving existing value if there is one (#42)
- [Feature] Sets MSBuild project path so properties like MSBuildThisFileDirectory work (#45, thanks @jirikopecky)

# 0.3.0

- **[Breaking Change]** [Refactoring] Added `AnalyzerManagerOptions` to encapsulate lesser used `AnalyzerManager` constructor arguments (#44)
- [Fix] Updated MSBuild API references for latest Visual Studio and .NET SDKs
- [Feature] Added support for custom build environments (#41, thanks @dfederm)
- [Feature] Added toggle for whether to clean when compiling (#38, #40, thanks @dfederm)

# 0.2.3

- [Feature] Added ability to tweak project files prior to build (#36, thanks @Mpdreamz)
- [Feature] Added ability to filter out specific projects in a solution (#35, thanks @Mpdreamz)
- [Fix] Extended timeout to get `dotnet --info` (#34, thanks @Mpdreamz)

# 0.2.2

- [Feature] Workspace extensions now accept `Workspace` instead of more specific `AdhocWorkspace` (#31, thanks @Jjagg)
- [Fix] Updated MSBuild API references (#32)

# 0.2.1

- [Fix] A better strategy for .NET Framework SDK projects (#23, #25)

# 0.2.0

- **[Breaking Change]** [Refactoring] Changed the `StringBuilder` logging arguments to take a `TextWriter` instead (#24)
- **[Breaking Change]** [Refactoring] Renamed `ProjectAnalyzer.ProjectPath` to `ProjectAnalyzer.ProjectFilePath` (and related method arguments) to make it clear this should be a file path
- [Feature] Allows passing a `XDocument` as a virtual project file (#19)
- [Feature] Adds an option to add known project references to the Roslyn workspace (#22)
- [Fix] Uses the VS toolchain for SDK .NET Framework projects (#23)

# 0.1.6

- [Fix] Ensures only projects are added when loading a solution (#14, #15, thanks @JosephWoodward)

# 0.1.5

- [Feature] Support for loading an entire solution into `AnalyzerManager` (#13)
- [Feature] Chooses the correct SDK folder depending on architecture of the host application (#10)
- [Feature] More test fixes for non-Windows platforms (#9, thanks @JosephWoodward)
- [Feature] Roslyn workspace reflects the correct `OutputKind` of the project (#8, thanks @JosephWoodward)

# 0.1.4

- [Feature] Roslyn workspaces now correctly resolve project references

# 0.1.3

- [Feature] Support for SDK projects with `Import` elements (#1, #6, thanks @mholo65)

# 0.1.2

- Unreleased, no idea where this version went

# 0.1.1

- [Fix] Fixed tests when not running on Windows because .NET Framework is unavailable (thanks @JosephWoodward)
- [Feature] Initial support for creating Roslyn workspaces

# 0.1.0

- Initial release