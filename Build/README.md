# Building and Using Jolt Physics

## Build Types

Each platform supports multiple build targets

- Debug - Debug version of the library, turns on asserts
- Release - Release version of the library, no asserts but includes profiling support and can draw the world and simulation properties
- ReleaseASAN - As Release but turns on Address Sanitizer (clang only) to find bugs
- ReleaseUBSAN - As Release but turns on Undefined Behavior Sanitizer (clang only) to find bugs
- ReleaseCoverage - As Release but turns on Coverage reporting (clang only) to find which areas of the code are not executed
- Distribution - Shippable version of the library, turns off all debugging support

## Includes

The Jolt headers don't include Jolt.h. Always include Jolt.h before including any other Jolt header.
You can use Jolt.h in your precompiled header to speed up compilation.

## Defines

There are a number of user configurable defines that turn on/off certain features:

- JPH_PROFILE_ENABLED - Turns on the internal profiler.
- JPH_EXTERNAL_PROFILE - Turns on the internal profiler but forwards the information to a user defined external system (see Profiler.h).
- JPH_DEBUG_RENDERER - Adds support to draw lines and triangles, used to be able to debug draw the state of the world.
- JPH_DISABLE_TEMP_ALLOCATOR - Disables the temporary memory allocator, used mainly to allow ASAN to do its job.
- JPH_FLOATING_POINT_EXCEPTIONS_ENABLED - Turns on division by zero and invalid floating point exception support in order to detect bugs (Windows only).
- JPH_USE_F16C - Enable half float CPU instructions (x64 only)
- JPH_USE_LZCNT - Enable the lzcnt CPU instruction (x64 only)
- JPH_USE_AVX - Enable AVX CPU instructions (x64 only)
- JPH_USE_AVX2 - Enable AVX2 CPU instructions (x64 only)
- JPH_USE_FMA - Enable fused multiply add CPU instructions (x64 only)

## Logging & Asserting

To override the default trace and assert mechanism install your own custom handlers in Trace and AssertFailed (see IssueReporting.h).

## Building

### Windows 10+ (CL - Default compiler)

- Download Visual Studio 2019+ (Community or other edition)
- Download CMake 3.15+ (https://cmake.org/download/)
- Run cmake_vs2019_cl.bat
- Open the resulting project file VS2019_CL\JoltPhysics.sln
- Compile and run either 'Samples' or 'UnitTests'

### Windows 10+ (Clang compiler)

- Download Visual Studio 2019+ (Community or other edition)
- Make sure to install "C++ Clang Compiler for Windows 11.0.0+" and "C++ Clang-cl for v142+ build tools (x64/x86)" using the Visual Studio Installer
- Download CMake 3.15+ (https://cmake.org/download/)
- Run cmake_vs2019_clang.bat
- Open the resulting project file VS2019_Clang\JoltPhysics.sln
- Compile and run either 'Samples' or 'UnitTests'

### Linux (Debian flavor, x64 or ARM64)

- Install clang (apt-get install clang)
- Install cmake (apt-get install cmake)
- Run: ./cmake_linux_clang.sh
- Go to the Linux_Debug folder
- Run: make -j 8 && ./UnitTests

### Android

- Install Android Studio 2020.3.1+ (https://developer.android.com/studio/)
- Open the 'Android' folder in Android Studio and wait until gradle finishes
- Select 'Run' / 'Run...' and 'UnitTests'
- If the screen turns green after a while the unit tests succeeded, when red they failed (see the android log for details)

## Unit Test Coverage Report on Windows

To test unit test coverage run the following:

- Run: cmake_vs2019_clang.bat
- Run: unit_tests_coverage.bat
- This will build and run the unit tests and open a browser with the results

## Doxygen

Documentation can be generated through doxygen:

- Install Doxygen (https://www.doxygen.nl/download.html)
- Install Microsoft HTML Help Workshop (to generate a CHM file)
- Run: run_doxygen.bat