# Reference 
# https://github.com/bemehiser/cmake_csharp_example
cmake_minimum_required(VERSION 3.8.2)
project("UnityLibExample" VERSION 0.1.0 LANGUAGES CSharp)

# Include CMake utilities for CSharp
include(CSharpUtilities)

# Set the C# language version (defaults to 3.0).
set(CMAKE_CSharp_FLAGS "/langversion:latest")

# Set .NET Framework version
set_property(GLOBAL PROPERTY VS_DOTNET_TARGET_FRAMEWORK_VERSION "v4.6.1")

# SET Custom variable 
set(UnityPath "C:/Program\ Files/Unity/Hub/Editor/2018.4.5f1" CACHE STRING "Path to Unity Installation")
set(MonoPath "C:/Program\ Files/Mono" CACHE STRING "Path to Mono Installation")

# Set Default to Debug
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug)
    message (STATUS "Setting CMAKE_BUILD_TYPE to Debug")
endif()

# Set "Install" (copy) path to Debug Proj
if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX ${PROJECT_SOURCE_DIR}/UnityDebugProj/Assets CACHE PATH "..." FORCE)
    message (STATUS "Setting CMAKE_INSTALL_PREFIX to " ${CMAKE_INSTALL_PREFIX})
endif()

# Find Unity Engine 
find_file(UnityEngineLibraries UnityEngine PATHS ${UnityPath} PATH_SUFFIXES "/Editor/Data/Managed" NO_DEFAULT_PATH)
if (NOT UnityEngineLibraries)
    message (FATAL_ERROR "Unity Engine Not Found!")
endif()
set(UnityEngineLibraries ${UnityEngineLibraries}.dll)
message (STATUS "Found UnityEngine: " ${UnityEngineLibraries})

# Find pdb2mdb
find_file(Pdb2mdbBat pdb2mdb PATHS ${MonoPath} PATH_SUFFIXES "/bin" NO_DEFAULT_PATH)
if ((CMAKE_BUILD_TYPE MATCHES Deb) AND (NOT Pdb2mdbBat))
    message (FATAL_ERROR "Mono pdb2mdb Not Found!")
endif()
set(Pdb2mdbBat ${Pdb2mdbBat}.bat)
message (STATUS "Found Pdb2mdb: " ${Pdb2mdbBat})

add_subdirectory(src)

