cmake_minimum_required(VERSION 3.5)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99 -Wno-unused-function")

project(clib)

set(EXECUTABLE_OUTPUT_PATH "${CMAKE_HOME_DIRECTORY}/${CMAKE_BUILD_TYPE}")

include_directories(deps src)

file(GLOB_RECURSE DEPS "deps/*.c")

set(CLIB_SOURCES
        src/clib.c
        ${DEPS}
        )

set(CLIB_SEARCH_SOURCES
        src/clib-search.c
        ${DEPS}
        )

set(CLIB_INSTALL_SOURCES
        src/clib-install.c
        ${DEPS}
        )

add_executable(clib ${CLIB_SOURCES})
add_executable(clib-search ${CLIB_SEARCH_SOURCES})
add_executable(clib-install ${CLIB_INSTALL_SOURCES})

target_link_libraries(clib curl)
target_link_libraries(clib-install curl)
target_link_libraries(clib-search curl)

# copy manifest to output
file(COPY ${CMAKE_HOME_DIRECTORY}/clib-install.exe.manifest
        DESTINATION ${EXECUTABLE_OUTPUT_PATH})

# copy package.json to output
file(COPY ${CMAKE_HOME_DIRECTORY}/package.json
        DESTINATION ${EXECUTABLE_OUTPUT_PATH})


# copy clib_install.at to output
file(COPY ${CMAKE_HOME_DIRECTORY}/clib.bat
        DESTINATION ${EXECUTABLE_OUTPUT_PATH})