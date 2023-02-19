cmake_minimum_required(VERSION 3.4)
project(antlr4_runtime)

include_directories(
  ${PROJECT_SOURCE_DIR}/src
  ${PROJECT_SOURCE_DIR}/src/atn
  ${PROJECT_SOURCE_DIR}/src/dfa
  ${PROJECT_SOURCE_DIR}/src/internal
  ${PROJECT_SOURCE_DIR}/src/misc
  ${PROJECT_SOURCE_DIR}/src/support
  ${PROJECT_SOURCE_DIR}/src/tree
  ${PROJECT_SOURCE_DIR}/src/tree/pattern
  ${PROJECT_SOURCE_DIR}/src/tree/xpath
)


file(GLOB libantlrcpp_SRC
  "${PROJECT_SOURCE_DIR}/src/*.cpp"
  "${PROJECT_SOURCE_DIR}/src/atn/*.cpp"
  "${PROJECT_SOURCE_DIR}/src/dfa/*.cpp"
  "${PROJECT_SOURCE_DIR}/src/internal/*.cpp"
  "${PROJECT_SOURCE_DIR}/src/misc/*.cpp"
  "${PROJECT_SOURCE_DIR}/src/support/*.cpp"
  "${PROJECT_SOURCE_DIR}/src/tree/*.cpp"
  "${PROJECT_SOURCE_DIR}/src/tree/pattern/*.cpp"
  "${PROJECT_SOURCE_DIR}/src/tree/xpath/*.cpp"
)

add_library(${PROJECT_NAME} STATIC ${libantlrcpp_SRC})
target_compile_definitions(${PROJECT_NAME} PUBLIC ANTLR4CPP_STATIC)
target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_SOURCE_DIR}/src)

find_package(Threads REQUIRED)
target_link_libraries(${PROJECT_NAME} Threads::Threads)


if(APPLE)
  find_library(COREFOUNDATION_LIBRARY CoreFoundation)
  target_link_libraries(${PROJECT_NAME} ${COREFOUNDATION_LIBRARY})
endif()