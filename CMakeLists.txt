################################################################################
### Programming language version and compiler flags
################################################################################
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(imgui CXX)

################################################################################
### Includes - source files, header files, moc files
################################################################################
file(GLOB IMGUI_HEADERS "*.h" "*.hpp")
file(GLOB IMGUI_SOURCES "*.cpp" "*.c")

set(IMGUI_INCLUDE_DIRS "/")
set(IMGUI_SOURCE_DIRS "/")

################################################################################
### Add build target
################################################################################
add_library(${PROJECT_NAME} STATIC ${IMGUI_HEADERS} ${IMGUI_SOURCES})

################################################################################
### Configure target
################################################################################
target_include_directories(${PROJECT_NAME} PUBLIC ${IMGUI_INCLUDE_DIRS} ${IMGUI_SOURCE_DIRS})

if(CMAKE_CXX_COMPILER_ID MATCHES "GNU" AND CMAKE_BUILD_TYPE MATCHES "Debug")
    target_compile_options(${PROJECT_NAME} PUBLIC 
                                    -Wall -fexceptions -std=c++17 -Wpedantic -Werror 
                                    -Wno-unknown-pragmas -Wno-unused-function -Oo)
    target_link_options(${PROJECT_NAME} PUBLIC -s)

elseif(CMAKE_CXX_COMPILER_ID MATCHES "GNU" AND CMAKE_BUILD_TYPE MATCHES "Release")
    target_compile_options(${PROJECT_NAME} PUBLIC 
                                    -Wall -fexceptions -std=c++17 -Wpedantic -Werror 
                                    -Wno-unknown-pragmas -Wno-unused-function -O3 -fPIC)
    target_link_options(${PROJECT_NAME} PUBLIC -s)

elseif(CMAKE_CXX_COMPILER_ID MATCHES "Clang" AND CMAKE_BUILD_TYPE MATCHES "Debug")
    target_compile_options(${PROJECT_NAME} PUBLIC 
                                    -Wall -fexceptions -std=c++17 -Wpedantic -Werror 
                                    -Wno-unknown-pragmas -Wno-unused-function -Oo)
    target_link_options(${PROJECT_NAME} PUBLIC -s)

elseif(CMAKE_CXX_COMPILER_ID MATCHES "Clang" AND CMAKE_BUILD_TYPE MATCHES "Release")
    target_compile_options(${PROJECT_NAME} PUBLIC 
                                    -Wall -fexceptions -std=c++17 -Wpedantic -Werror 
                                    -Wno-unknown-pragmas -Wno-unused-function -O3 -fPIC)
    target_link_options(${PROJECT_NAME} PUBLIC -s)

elseif(CMAKE_CXX_COMPILER_ID MATCHES "MSVC" AND CMAKE_BUILD_TYPE MATCHES "Debug")
    target_compile_options(${PROJECT_NAME} PUBLIC 
                                    /W4 /WX- /permissive- /std:c++17
                                    /TP /Gd /Gm- /RTC0 /diagnostics:classic
                                    /fp:precise /EHsc)
    target_link_options(${PROJECT_NAME} PUBLIC /INCREMENTAL /MACHINE:X64)

elseif(CMAKE_CXX_COMPILER_ID MATCHES "MSVC" AND CMAKE_BUILD_TYPE MATCHES "Release")
    target_compile_options(${PROJECT_NAME} PUBLIC 
                                    /W4 /WX- /permissive- /std:c++17
                                    /TP /Gd /Gm- /diagnostics:classic
                                    /fp:precise /EHsc /Ob2 /Ox /Oi)
    target_link_options(${PROJECT_NAME} PUBLIC /INCREMENTAL /MACHINE:X64)
endif()