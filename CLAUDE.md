# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

Docker images used by Emgu Corporation to build releases of [Emgu CV](https://github.com/emgucv/emgucv) (an OpenCV wrapper for .NET) and related projects. Each subdirectory is an independent Docker image definition.

## Building Images

### Linux images
```bash
# Standard build
docker build -t emgu/<image-name> .

# Cross-platform ARM build (bazel-debian-arm only)
docker buildx build --platform linux/arm/v7 -t emgu/bazel-debian-arm .
```

### Windows images (require 8GB memory)
```batch
docker build -t emgu/<image-name> -m 8G .
```

Each directory contains a `docker_build` (Linux) or `docker_build.bat` (Windows) script with the exact command for that image.

## Image Inventory

| Directory | Base OS | Key Tools | Target Platform |
|---|---|---|---|
| `bazel-android` | Ubuntu 24.04 | Bazelisk 1.20.0, OpenJDK 21, Android SDK/NDK, .NET 10.0, Emscripten | Android/WASM cross-compile |
| `bazel-debian-arm` | Debian Bullseye | Bazel 4.2.1 (built from source), OpenJDK 17, .NET 6.0 | Linux ARM 32-bit |
| `bazel-debian-arm64` | Debian Bookworm | Bazel 6.4.0 (pre-built), OpenJDK 17, .NET 7.0 | Linux ARM64 |
| `bazel-ubuntu-arm64` | Ubuntu 20.04 | Bazel 4.0.0 (built from source), OpenJDK 17, .NET 6.0 | Linux ARM64 (Ubuntu) |
| `buildbot` | Ubuntu 24.04 | Buildbot master, Apache2, ClamAV | CI/CD master server |
| `ubi-x64` | Red Hat UBI 9 | GCC, .NET 10.0, Mono, OpenCV deps | RHEL-compatible x64 |
| `vs2019_buildtools` | Windows Server 2019 | VS2019 16.11.0, Chocolatey, MSYS2, Android SDK | Windows x64 base |
| `vs2019_buildtools_cuda` | `emgu/vs2019_buildtools` | CUDA 11.4.1, CUDNN | Windows + GPU |
| `vs2019_buildtools_cuda_openvino` | `emgu/vs2019_buildtools_cuda` | OpenVINO 2021.4.582 | Windows + AI inference |
| `vs2019_buildtools_cuda_bazel` | `emgu/vs2019_buildtools_cuda_openvino` | Bazel 4.2.1, .NET 6.0 | Windows + Bazel |

## Image Dependency Chain (Windows)

```
vs2019_buildtools
  └── vs2019_buildtools_cuda
        └── vs2019_buildtools_cuda_openvino
              └── vs2019_buildtools_cuda_bazel
```

When rebuilding Windows images, rebuild from the root of the chain downward if changing a base image.

## Key Notes

- **`bazel-debian-arm`**: Bazel must be compiled from source with an ARM patch because no pre-built ARM binary is available for that version.
- **`vs2019_buildtools_cuda`**: CUDNN and Video Codec SDK files must be manually copied into the build context before building (they cannot be downloaded automatically).
- **`ubi-x64`**: Sets `OPENSSL_ENABLE_SHA1_SIGNATURES=1` for Emgu CV compatibility. Uses EPEL repository for additional packages.
- **`buildbot`**: Runs Buildbot in a Python venv at `/opt/buildbot`.
- The `Install.cmd` script in `vs2019_buildtools` wraps VS installer calls and collects diagnostic logs on failure; exit code 3010 (reboot required) is treated as success.
