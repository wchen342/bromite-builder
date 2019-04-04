# Bromite Builder

Utility script for building [Bromite]( https://github.com/bromite/bromite) releases

- [Requirements](#requirements)
- [Setup](#setup)
- [Usage](#usage)
- [Notes](#notes)
- [Resources](#resources)

## <a name="requirements"></a>Requirements

- A 64-bit Intel machine running Linux with at least 8GB of RAM.
More than 16GB is highly recommended.
- At least 100GB of free disk space.
- You must have Git and Python 2 installed already.

## <a name="setup"></a>Setup

Ubuntu users' systems will be bootstrapped via Chromium's
[`build/install-build-deps-android.sh`](https://chromium.googlesource.com/chromium/src.git/+/master/build/install-build-deps-android.sh)

All other distro users should follow Chromium's
[Notes For Other Distros](https://chromium.googlesource.com/chromium/src/+/master/docs/linux_build_instructions.md#notes)

Checking out the repo:
```shell
git clone git@github.com:nikolowry/bromite-builder; \
cd bromite-builder
```

## <a name="usage"></a>Usage

Usage instructions are always available by running `./bromite-builder -h` or
`./bromite-builder --help`

```
Usage: ./bromite-builder [command...] [options...]

Where optional [command] is one of:
    build, clean, fetch-sync, prepare, set-revision

If no [command] is set, the default command sequence will be executed:
    - set-revision
    - fetch-sync
    - prepare
    - build

Options:
    -a, --arch=<arch>            Where <arch> is: arm, arm64, x86. Defaults to arm
    -g, --gn-args=<args>         Where <args> is a string of GN build arguments
    -p, --patches-dir=<dir>      Where <dir> is a path to a directory containing custom patches
    -t, --target=<target>        Where Ninja <target> is: chrome_modern_public_apk, chrome_public_apk, monochrome_public_apk. Defaults to chrome_modern_public_apk
    -r, --revision=<revision>    Where <revision> is a Bromite release tag. Defaults to Bromite's latest release.
    --upstream                   Use Bromite's git source instead of a release tag. If set, any Chromium tag can be assigned to <revision>
    --dark-navbar                Prefer a dark navigation bar over a white one
    --no-javalite                Use Protobuf's full Java code generator instead of Java Lite
    -h, --help                   Print help menu
```

## <a name="notes"></a>Notes

Builds produced with `bromite-builder` differ from official Bromite releases with
the following:

- Retains Chromium branding and namespace
- Symbols are turned off for faster build times. For even faster builds on
`arm64` and `x86`, build with option `--gn-args="use_jumbo_build=true"
`- Optionally revert the white Navigation Bar in the Material Design Refresh (MD2)
to black with option `--dark-navbar`
- Optionally prefer Protobuf's full Java runtime with option `--no-javalite`

## <a name="resources"></a>Resources

- Bromite Repo: https://github.com/bromite/bromite
- Ungoogled Chromium Repo: https://github.com/Eloston/ungoogled-chromium
- Chromium Repo: https://chromium.googlesource.com/chromium/src.git/
- Chromium Android Build Docs: https://chromium.googlesource.com/chromium/src/+/master/docs/android_build_instructions.md
