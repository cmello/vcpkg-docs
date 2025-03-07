---
title: vcpkg_install_msbuild
description: Learn how to use vcpkg_install_msbuild.
ms.date: 11/30/2022
---
# vcpkg_install_msbuild

> [!WARNING]
> This function has been deprecated in favor of [`vcpkg_msbuild_install`](vcpkg_msbuild_install.md).

Build and install a msbuild-based project. This replaces `vcpkg_build_msbuild()`.

## Usage

```cmake
vcpkg_install_msbuild(
    SOURCE_PATH <${SOURCE_PATH}>
    PROJECT_SUBPATH <port.sln>
    [INCLUDES_SUBPATH <include>]
    [LICENSE_SUBPATH <LICENSE>]
    [RELEASE_CONFIGURATION <Release>]
    [DEBUG_CONFIGURATION <Debug>]
    [TARGET <Build>]
    [TARGET_PLATFORM_VERSION <10.0.15063.0>]
    [PLATFORM <Win32>]
    [PLATFORM_TOOLSET <v143>]
    [OPTIONS </p:ZLIB_INCLUDE_PATH=X>...]
    [OPTIONS_RELEASE </p:ZLIB_LIB=X>...]
    [OPTIONS_DEBUG </p:ZLIB_LIB=X>...]
    [USE_VCPKG_INTEGRATION]
    [ALLOW_ROOT_INCLUDES | REMOVE_ROOT_INCLUDES]
)
```

## Parameters

### SOURCE_PATH
The path to the root of the source tree.

Because MSBuild uses in-source builds, the source tree will be copied into a temporary location for the build. This
parameter is the base for that copy and forms the base for all XYZ_SUBPATH options.

### USE_VCPKG_INTEGRATION

Apply the normal `integrate install` integration for building the project.

By default, projects built with this command will not automatically link libraries or have header paths set.

### PROJECT_SUBPATH

The subpath to the solution (`.sln`) or project (`.vcxproj`) file relative to `SOURCE_PATH`.

### LICENSE_SUBPATH

The subpath to the license file relative to `SOURCE_PATH`.

### INCLUDES_SUBPATH

The subpath to the includes directory relative to `SOURCE_PATH`.

This parameter should be a directory and should not end in a trailing slash.

### ALLOW_ROOT_INCLUDES

Indicates that top-level include files (e.g. `include/zlib.h`) should be allowed.

### REMOVE_ROOT_INCLUDES

Indicates that top-level include files (e.g. `include/Makefile.am`) should be removed.

### SKIP_CLEAN

Indicates that the intermediate files should not be removed.

Ports using this option should later call [`vcpkg_clean_msbuild()`](vcpkg_clean_msbuild.md) to manually clean up.

### RELEASE_CONFIGURATION

The configuration (`/p:Configuration` msbuild parameter) used for Release builds.

### DEBUG_CONFIGURATION

The configuration (`/p:Configuration` msbuild parameter) used for Debug builds.

### TARGET_PLATFORM_VERSION

The WindowsTargetPlatformVersion (`/p:WindowsTargetPlatformVersion` msbuild parameter).

### TARGET

The MSBuild target to build (`/t:<TARGET>`).

### PLATFORM

The platform (`/p:Platform` msbuild parameter) used for the build.

This defaults to a value mapping `VCPKG_TARGET_ARCHITECTURE` to the default values Visual Studio uses when creating a `.vcxproj`:

* `x86` becomes `Win32`
* `x64` becomes `x64`
* `arm` becomes `ARM`
* `arm64` becomes `arm64`

When passing a `.sln` rather than a `.vcxproj`, this may need to be set back to `${VCPKG_TARGET_ARCHITECTURE}` to match the Platform strings used by solutions.

### PLATFORM_TOOLSET

The platform toolset (`/p:PlatformToolset` msbuild parameter) used for the build.

### OPTIONS

Additional options passed to msbuild for all builds.

### OPTIONS_RELEASE

Additional options passed to msbuild for Release builds. These are in addition to `OPTIONS`.

### OPTIONS_DEBUG

Additional options passed to msbuild for Debug builds. These are in addition to `OPTIONS`.

## Source

[scripts/cmake/vcpkg\_install\_msbuild.cmake](https://github.com/Microsoft/vcpkg/blob/master/scripts/cmake/vcpkg_install_msbuild.cmake)

