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

## Running it

Go to **Actions → Build exhale (MSYS2 CLANG64) → Run workflow**.

You can optionally set the **ref** input to a specific exhale tag, branch, or commit hash. Leave it blank to build the default branch (`master`).

The workflow also runs automatically on push to `main` and on a weekly schedule, so it periodically picks up new exhale releases.

## Getting the binary

After a run finishes, download the `exhale-<version>-clang64` artifact from the workflow run's **Artifacts** section. It contains a single stripped `exhale.exe`.

## Credit

All encoder source code and licensing belong to the upstream [ecodis/exhale](https://gitlab.com/ecodis/exhale) project by Christian R. Helmrich. This repository only automates building it; see the upstream repository for usage instructions and license terms.
