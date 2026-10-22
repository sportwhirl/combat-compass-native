# Build Combat Compass Native 0.2.2

The repository's ZIP contains the complete native source bundle and local build glue. Download and extract [CombatCompass-0.2.2-Native-Source.zip](CombatCompass-0.2.2-Native-Source.zip), then run the commands below from the extracted bundle root (the folder containing `experiments/`, `native/`, and `vendor/`).

## Requirements

The recorded build uses a Linux host and cross-compiles a Windows x64 plugin. Install these tools and make them available on `PATH`:

- clang-cl 23.1.1
- lld-link
- llvm-lib
- llvm-rc
- llvm-mt
- Ninja
- CMake 3.24 or newer (the recorded build used 4.4.4)
- Python 3

You also need a separately licensed Microsoft Visual C++ runtime and Windows SDK sysroot staged at:

```text
vendor/native-build/windows-sysroot
```

The sysroot must include the CRT and Windows SDK headers and libraries. The compiler, SDK files, and Skyrim game data are not included in the source archive. The toolchain file stops with an error if the expected sysroot directories are missing.

## Build

From the extracted bundle root, run:

```bash
bash experiments/latest-runtime/build_windows.sh
```

The script configures and builds the bundled dependencies and plugin with CMake and Ninja. It writes the plugin here:

```text
build/native-latest-windows/CombatCompass.dll
```

The script includes a small compatibility correction for two tokens in the bundled DirectXTK SimpleMath header before building.

## Compatibility and notes

The plugin entry point supports Skyrim SE 1.6.1170 and 1.7.104. The native code supports Address Library format 5 and legacy format 2. Address Library files and game executables are not included; supply your own matching files only if performing address-probe testing.

The Papyrus source is included at `papyrus/RN_Controller.psc`, but Papyrus compilation is separate from the native DLL build. It requires the Bethesda Papyrus compiler and matching game, SKSE, PapyrusUtil, UIExtensions, and other mod script includes supplied separately.

The native plugin and combined DLL use GPL-3.0-or-later with the included CommonLib exceptions. Keep the included license and exception documents with the source. Third-party source retains its own license.
