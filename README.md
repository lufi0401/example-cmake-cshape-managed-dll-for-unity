# Example CMake C# Project for generating Managed DLL for Unity

# Compile Instruction
1. 
```bash 
mkdir build
cd build
cmake .. -G"Visual Studio 15 2017"

# If using VS Developer Console; otherwise use 2-3
devenv /build Debug UnityLibExample.sln
```
2. Open build/UnityLibExample.sln file in Visual Studio
3. Build ALL_BUILD and INSTALL

4. Run Unity Project and see the script in Assets/bin

