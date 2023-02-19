This project includes only the ANTLR4 runtime for C++.

Right now it can only be linked statically.

Example:
```cmake
add_subdirectory(antlr4_cpp_runtime)
target_link_libraries(${PROJECT_NAME} antlr4_runtime)
```