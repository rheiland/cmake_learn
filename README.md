# cmake_learn

Just as the repo name states, I'm trying to learn the basics of cmake.

Usage:

clone this repo, then (on OSX/Linux):
```
cd <repo>
mkdir build
cd build
cmake ..
```
or if you want to specify different compilers than the default, use e.g.:
```
cmake -DCMAKE_CXX_COMPILER=g++-7 -DCMAKE_C_COMPILER=gcc-7 ..
```
Assuming the cmake is successful, you then just run:
```
make
```
On Windows 10, after installing Visual Studio 17 (VS17; free Community edition), I run a batch script (.bat) as follows:
```
cmd.exe /k ""c:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Auxiliary\Build\vcvarsall.bat" x64 & powershell"
```
which seems to do some magic of making my Command Prompt shell know about the VS17 "cl" compiler (and put my Command Prompt into "Powershell" mode so I'll have more Unix-like commands). And then I run "cmake .." and "make".
