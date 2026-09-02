# exhale Windows Builds

This repository builds Windows binaries of [exhale](https://gitlab.com/ecodis/exhale), the ecodis Extended HE-AAC (USAC) encoder, using GitHub Actions.

exhale's source lives on GitLab, not here — the workflow clones it fresh, compiles it with MSYS2/Clang (CLANG64 environment), strips debug symbols, and uploads the resulting `exhale.exe` as a workflow artifact.

## How it works

The workflow (`.github/workflows/build-exhale.yml`) does the following on a Windows runner:

1. Sets up an MSYS2 CLANG64 environment with `clang`, `cmake`, and `ninja`.
2. Clones `https://gitlab.com/ecodis/exhale.git`.
3. Resolves a version string from the checked-out git tag/commit (used to name the artifact).
4. Configures and builds with CMake (`-static -O3`, Release mode) and strips the resulting binary.
5. Uploads `exhale.exe` as a build artifact.

## Credit

All encoder source code and licensing belong to the upstream [ecodis/exhale](https://gitlab.com/ecodis/exhale) project by Christian R. Helmrich. This repository only automates building it; see the upstream repository for usage instructions and license terms.
