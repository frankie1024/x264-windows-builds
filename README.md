# x264 Windows Builds

This repository builds Windows x64 executable packages from the official
[x264](https://code.videolan.org/videolan/x264) VideoLAN repository.

x264 does not publish GitLab releases in the same way SVT-AV1 does. This
workflow follows the official `stable` branch and publishes a new GitHub
release whenever the upstream `stable` commit changes.

The generated release tag format is:

```text
stable-YYYYMMDD-<short-sha>
```

## Output

Each GitHub release contains:

- `x264.exe`
- `BUILD_INFO.txt` with the source branch, commit, and build settings

The packaged archive name is:

```text
x264-<tag>-windows-x64.zip
```

## Manual Build

Open the `Build x264 Windows x64` workflow and run it with:

- `ref`: optional upstream branch, tag, or commit. Empty means `stable`.
- `force`: rebuild and replace release assets if the GitHub release already exists.

For a fixed upstream ref, the GitHub release tag is still generated from the
resolved commit.

## Build Details

The GitHub Actions job runs on `windows-2022` and uses MSYS2 MinGW x64:

```bash
git clone https://code.videolan.org/videolan/x264.git
git checkout <resolved-commit>
./configure --host=x86_64-w64-mingw32 --enable-static --disable-opencl --disable-lavf --disable-ffms --disable-gpac --disable-lsmash
make -j$(nproc)
```

The final CLI executable is packaged as `x264.exe`.

## Upstream Licenses

This repository only contains automation. Built x264 binaries are subject to
the upstream x264 license terms. See the upstream project:

- https://code.videolan.org/videolan/x264
