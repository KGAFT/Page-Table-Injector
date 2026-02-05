cmake_minimum_required(VERSION 3.21)
project(PtDriver-UM)

add_subdirectory(external)

# Force clang-cl
set(CMAKE_C_COMPILER clang-cl)
set(CMAKE_CXX_COMPILER clang-cl)

set(CMAKE_CXX_STANDARD 20)


link_directories(
    "${WDK_ROOT}/Lib/${WDK_VERSION}/um/x64"
)

file(GLOB_RECURSE SRC_FILES src/*.*)



add_executable(PtDriver-um ${SRC_FILES})

target_include_directories(PtDriver-um PUBLIC src/ "${WDK_ROOT}/Include/${WDK_VERSION}/um"
        "${WDK_ROOT}/Include/${WDK_VERSION}/shared")


target_link_libraries(PtDriver-um
    kernel32.lib
    user32.lib
    advapi32.lib
    ntdll.lib
    DIA
)