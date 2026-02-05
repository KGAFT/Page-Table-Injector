cmake_minimum_required(VERSION 3.30)

project(injector)

set(WDK_ROOT "C:/Program Files (x86)/Windows Kits/10")
set(WDK_VERSION "10.0.26100.0")

add_subdirectory(client)
add_subdirectory(driver)
