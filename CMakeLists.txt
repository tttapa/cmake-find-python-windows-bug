cmake_minimum_required(VERSION 3.26)

# Cross-compilation for ARM
set(CMAKE_SYSTEM_NAME Windows)
set(CMAKE_SYSTEM_PROCESSOR ARM64)
set(CMAKE_GENERATOR_PLATFORM ARM64)
project(find-python)

# Download Python for ARM using NuGet
set(NUGET_PYTHON_VERSION "3.12.7" CACHE STRING "Version of Python to download")
if (NOT IS_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/pythonarm64.${NUGET_PYTHON_VERSION})
    execute_process(COMMAND nuget install pythonarm64 -Version ${NUGET_PYTHON_VERSION}
                            -FallbackSource https://api.nuget.org/v3/index.json
                            -OutputDirectory ${CMAKE_CURRENT_BINARY_DIR})
endif()

# FindPython
set(Python_ROOT_DIR ${CMAKE_CURRENT_BINARY_DIR}/pythonarm64.${NUGET_PYTHON_VERSION}/tools
    CACHE PATH "" FORCE)
if (FALSE)
    # Works
    find_package(Python 3.8 REQUIRED COMPONENTS Development.Module)
else()
    # Broken
    find_package(Python 3.8 REQUIRED COMPONENTS Development.Module
                            OPTIONAL_COMPONENTS Development.SABIModule)
endif()
