cmake_minimum_required(VERSION 3.16)

project(
    ccli
    VERSION 0.0.0
    DESCRIPTION "Portable CLI framework."
    LANGUAGES C
)

# Export compile commands database for `clang-tidy`.
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Set up the `ccli` library target.
add_library(ccli SHARED src/test.c)

# Set up the test executable target.
add_executable(tests tests/test.c)
find_library(CMOCKA_LIBRARY cmocka REQUIRED)
target_link_libraries(tests PRIVATE ${CMOCKA_LIBRARY} ccli)

# Set up automatic packaging.
set(CPACK_PACKAGE_VENDOR "H Paterson")
set(CPACK_PACKAGE_CONTACT "H Paterson <harley.paterson@postgrad.otago.ac.nz>")
set(CPACK_PACKAGE_DESCRIPTION "Portable CLI framework.")
set(CPACK_PACKAGE_VERSION_MAJOR ${PROJECT_VERSION_MAJOR})
set(CPACK_PACKAGE_VERSION_MINOR ${PROJECT_VERSION_MINOR})
set(CPACK_PACKAGE_VERSION_PATCH ${PROJECT_VERSION_PATCH})
set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/LICENCE.txt")
set(CPACK_RESOURCE_FILE_README "${CMAKE_CURRENT_SOURCE_DIR}/README.md")
include(CPack)
