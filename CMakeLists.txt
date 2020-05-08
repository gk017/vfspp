cmake_minimum_required(VERSION 2.8)
include(ExternalProject)
set_property (GLOBAL PROPERTY USE_FOLDERS ON)

project(vfspp)
set(VERSION "1.0.0")

# Target name
set(target vfspp)

# Exit here if required dependencies are not met
message(STATUS "Lib ${target}")

# Sources
set(sources
        CFileInfo.h
        CMemoryFile.h
        CMemoryFileSystem.h
        CStringUtilsVFS.h
        CVirtualFileSystem.h
        IFile.h
        IFileSystem.h
        VFS.h
        CFileInfo.cpp
        CMemoryFile.cpp
        CMemoryFileSystem.cpp
        CStringUtilsVFS.cpp
        CVirtualFileSystem.cpp
        )


# Create library
add_library(${target} SHARED
        ${sources}
        )

# Project options
set_target_properties(${target}
        PROPERTIES
        ${DEFAULT_PROJECT_OPTIONS}
        FOLDER "${IDE_FOLDER}"
        )

# Include directories
target_include_directories(${target}
        PRIVATE
        ${DEFAULT_INCLUDE_DIRECTORIES}
        ${PROJECT_BINARY_DIR}/source/include
        )

# Libraries
target_link_libraries(${target}
        PRIVATE
        ${DEFAULT_LIBRARIES}

        )

# Compile definitions
target_compile_definitions(${target}
        PRIVATE
        ${DEFAULT_COMPILE_DEFINITIONS}
        )

# Compile options
target_compile_options(${target}
        PRIVATE
        ${DEFAULT_COMPILE_OPTIONS}
        )

# Linker options
target_link_libraries(${target}
        PRIVATE
        ${DEFAULT_LINKER_OPTIONS}
        )

