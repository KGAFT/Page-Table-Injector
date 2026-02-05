cmake_minimum_required(VERSION 3.21)
project(PtDriver)

# Force clang-cl
set(CMAKE_C_COMPILER clang-cl)
set(CMAKE_CXX_COMPILER clang-cl)

# WDK paths
set(WDK_ROOT "C:/Program Files (x86)/Windows Kits/10")
set(WDK_VERSION "10.0.26100.0")



# Kernel libs
link_directories(
    "${WDK_ROOT}/Lib/${WDK_VERSION}/km/x64"
)


file(GLOB_RECURSE SRC_FILES src/*.*)

add_executable(PtDriver ${SRC_FILES})

target_include_directories(PtDriver PUBLIC src/ "${WDK_ROOT}/Include/${WDK_VERSION}/km"
        "${WDK_ROOT}/Include/${WDK_VERSION}/shared")

# Kernel compile flags
target_compile_options(PtDriver PRIVATE
        -ffreestanding
        -fno-exceptions
        -fno-rtti
        -fno-stack-protector
        -fno-builtin
        -mno-red-zone

        -D_KERNEL_MODE
        -DWIN32
        -D_AMD64_

        /EHs-
        /EHc-
        /GR-
)

# Kernel link flags
set_target_properties(PtDriver PROPERTIES
    SUFFIX ".sys"
    LINK_FLAGS "/DRIVER /SUBSYSTEM:NATIVE /ENTRY:entry"
)



target_link_libraries(PtDriver 
    ntoskrnl.lib
    hal.lib
    wmilib.lib
)
