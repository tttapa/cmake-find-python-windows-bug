cmake_minimum_required(VERSION 3.26)
project(find-python)

option(WITH_SABI
       "Locate Development.SABIModule component in addition to Development.Module" On)
if (WITH_SABI)
    # Broken
    find_package(Python 3.8 REQUIRED COMPONENTS Development.Module
                            OPTIONAL_COMPONENTS Development.SABIModule)
else()
    # Works
    find_package(Python 3.8 REQUIRED COMPONENTS Development.Module)
endif()
