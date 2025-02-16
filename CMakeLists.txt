### YOU CAN'T MODIFY THE CODE BELOW
cmake_minimum_required(VERSION 3.10.2)
project(python_interpreter)
set(CMAKE_CXX_STANDARD 14)
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g")
include_directories(
        ${PROJECT_SOURCE_DIR}/generated/
        ${PROJECT_SOURCE_DIR}/third_party/
        ${PROJECT_SOURCE_DIR}/third_party/runtime/src
        ${PROJECT_SOURCE_DIR}/src/
)
set(src_dir
        ${PROJECT_SOURCE_DIR}/generated/Python3Lexer.cpp
        ${PROJECT_SOURCE_DIR}/generated/Python3Parser.cpp
        ${PROJECT_SOURCE_DIR}/generated/Python3Listener.cpp
        ${PROJECT_SOURCE_DIR}/generated/Python3BaseListener.cpp
        )
file(GLOB antlr4-cpp-src
        ${PROJECT_SOURCE_DIR}/third_party/runtime/src/*.cpp
        ${PROJECT_SOURCE_DIR}/third_party/runtime/src/atn/*.cpp
        ${PROJECT_SOURCE_DIR}/third_party/runtime/src/dfa/*.cpp
        ${PROJECT_SOURCE_DIR}/third_party/runtime/src/misc/*.cpp
        ${PROJECT_SOURCE_DIR}/third_party/runtime/src/support/*.cpp
        ${PROJECT_SOURCE_DIR}/third_party/runtime/src/tree/*.cpp
        ${PROJECT_SOURCE_DIR}/third_party/runtime/src/tree/pattern/*.cpp
        ${PROJECT_SOURCE_DIR}/third_party/runtime/src/tree/xpath/*.cpp
        )
add_library (antlr4-cpp-runtime ${antlr4-cpp-src})
### YOU CAN"T MODIFY THE CODE ABOVE

include_directories(
        ${PROJECT_SOURCE_DIR}/include
        ${PROJECT_SOURCE_DIR}/third_party/int2048_by_DarkSharpness/include   
)
file(GLOB int2048-src
        ${PROJECT_SOURCE_DIR}/third_party/int2048_by_DarkSharpness/src/int2048.cpp
)
add_library(int2048-runtime ${int2048-src})

set(pyinter_src_dir
        ${PROJECT_SOURCE_DIR}/src/main.cpp
        ${PROJECT_SOURCE_DIR}/src/Evalvisitor.cpp
        ${PROJECT_SOURCE_DIR}/src/exception.cpp
        ${PROJECT_SOURCE_DIR}/src/scope.cpp
        ${PROJECT_SOURCE_DIR}/src/utils.cpp
)

# add_executable(code ${src_dir} ${pyinter_src_dir})

# target_link_libraries(code antlr4-cpp-runtime int2048-runtime)

add_executable(pyinter ${src_dir} ${pyinter_src_dir})

target_link_libraries(pyinter antlr4-cpp-runtime int2048-runtime)

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)
