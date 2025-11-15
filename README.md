# Far Cry
Source code of Far Cry 1 which was leaked 24 june 2023.
https://archive.org/details/far-cry-1.34-complete

 ## Build

 Only the CMake build system is supported. Visual Studio solution files have been removed in favor of `CMakeLists.txt` and `CMakePresets.json`.

 ```
 cmake -S . -B build -G "Ninja" -DCMAKE_BUILD_TYPE=Debug
 cmake --build build
 ```

 Use `-DCMAKE_BUILD_TYPE=Release` (or an appropriate preset) for non-Debug builds.

 ## Changes

 * Migrated the project to build exclusively with CMake (currently validated on Win32 Debug)
* Replaced DXSDK to June 2010 version

Code changes:
* Most stdafx.h files - Added _SILENCE_STDEXT_HASH_DEPRECATION_WARNINGS
* CryCommon - IScriptSystem.h: Moved some methods from WIN64 macro
* CrySystem - MTSafeAllocator.h: replaced old std methods
* CrySystem  - HTTPDownloader.cpp: commented 309-310 lines
* CryAnimation - disabled UNIQUE_VERT_BUFF_PER_INSTANCE becase of weird buffer descrution
* CryAnimation - CryModel.cpp: 79 line commented becase of weird buffer descrution
* CryNetwork - Disabled ubisoft nerwork code
* CryGame - ScriptObjectGame.cpp: 2718 line commented save loading
* XRenderD3D9 - Replaced DxErr9 with DxErr from lastest DXSDK
* XRenderD3D9 - removed assert on invalid sector vertex buffer

### TODO:
* Replace nvDXT with nvtt
* Remove nvidia cg
* Fix bugs ...

### TODO FUTURE:
* Port engine to SDL
* Port engine to Linux
* Rewrite renderer to bgfx/Diligent Engine/NVRHI