cmake_minimum_required(VERSION 3.10)
project(sqlite3)

set(CMAKE_C_STANDARD 99)

set(SOURCE_FILES src/sqlite3.c src/sqlite3.h src/sqlite3ext.h)
if(WIN32)
    set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR}/windows)
    add_library(sqlite3 SHARED ${SOURCE_FILES})
    target_compile_definitions(sqlite3 PRIVATE -DSQLITE_API=__declspec(dllexport))
    set_target_properties(sqlite3 PROPERTIES OUTPUT_NAME "sqlite3")

else()
    set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR}/linux)
    add_library(sqlite3 SHARED ${SOURCE_FILES})
    target_compile_definitions(sqlite3 PRIVATE -DSQLITE_API=)
    set_target_properties(sqlite3 PROPERTIES OUTPUT_NAME "libsqlite3")
endif()


set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${LIBRARY_OUTPUT_PATH})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${LIBRARY_OUTPUT_PATH})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${LIBRARY_OUTPUT_PATH})
