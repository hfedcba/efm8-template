# Setup toolchain

## IDE

It is recommended to use JetBrains CLion for this project.

## Windows

1. Download the toolchain from https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/downloads (AArch32 bare-metal target, executable file).
2. Install the toolchain to the default location.
3. Fix toolchain path in `CMakeLists.txt` if required.
4. Download and install SEGGER J-Link from https://www.segger.com/downloads/jlink/.
5. Add `C:\Program Files\SEGGER\JLink` to the system's `Path` variable.
6. In CLion set MinGW as toolchain.
7. Add `Embedded GDB Server` to debug configurations.
8. Set `Target` to `flash`, `Executable` to the built binary file (the file matching the project name without file ending).
9. Set `GDB` to `Bundled GDB`.
10. Set `target remote args` to `tcp:localhost:2331`.
11. Set `GDB Server` to `C:\Program Files\SEGGER\JLink\JLinkGDBServer.exe`.
12. Set `GDB Server args` to `-device EFM32PG22C200F512IM40 -speed 4000 -if SWD`.
13. Add `Build` to `Before launch`.

## Linux

1. Download the toolchain from https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/downloads (AArch32 bare-metal target, `.tar.xz` file).
2. Extract the toolchain to `/usr/src/`.
3. Fix toolchain path in `CMakeLists.txt` if required.
4. Download and install SEGGER J-Link from https://www.segger.com/downloads/jlink/.
5. In CLion use the default toolchain.
6. Add `Embedded GDB Server` to debug configurations.
7. Set `Target` to `flash`, `Executable` to the built binary file (the file matching the project name without file ending).
8. Set `GDB` to `Bundled GDB`.
9. Set `target remote args` to `tcp:localhost:2331`.
10. Set `GDB Server` to `/usr/bin/JLinkGDBServerExe`.
11. Set `GDB Server args` to `-device EFM32PG22C200F512IM40 -speed 4000 -if SWD`.
12. Add `Build` to `Before launch`.

# Examples

https://github.com/SiliconLabs/peripheral_examples/tree/master/series2
