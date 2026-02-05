cmake_minimum_required(VERSION 3.30)

project(DIA)

add_library(DIA SHARED IMPORTED GLOBAL)

set_target_properties(DIA PROPERTIES
        IMPORTED_IMPLIB
        "${CMAKE_CURRENT_LIST_DIR}/DIA/lib/x64/diaguids.lib"

        IMPORTED_LOCATION
        "${CMAKE_CURRENT_LIST_DIR}/DIA/bin/x64/msdia140.dll"

        INTERFACE_INCLUDE_DIRECTORIES
        "${CMAKE_CURRENT_LIST_DIR}/DIA/include"
)