cmake_minimum_required(VERSION 3.28)
project(my_project)

# GoogleTest requires at least C++14
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_FLAGS_DEBUG "-Wall -Wextra -Wshadow -Wnon-virtual-dtor -Wunreachable-code -pedantic -Wold-style-cast -Wcast-align -Wunused -Woverloaded-virtual -Wconversion -Wsign-conversion -Wdouble-promotion -Wformat=2 -Werror -g -O0")
set(CMAKE_CXX_FLAGS_RELEASE "-Wall -Wextra -Wshadow -Wnon-virtual-dtor -Wunreachable-code -pedantic -Wold-style-cast -Wcast-align -Wunused -Woverloaded-virtual -Wconversion -Wsign-conversion -Wdouble-promotion -Wformat=2 -Werror -O3")

add_compile_options(-fsanitize=address)
add_link_options(-fsanitize=address)
add_compile_options(-fsanitize=pointer-compare)
add_link_options(-fsanitize=pointer-compare)
add_compile_options(-fsanitize=pointer-subtract)
add_link_options(-fsanitize=pointer-subtract)
add_compile_options(-fsanitize-address-use-after-scope)
add_link_options(-fsanitize-address-use-after-scope)

#add_compile_options(-fsanitize=memory -fPIE -pie)
#add_link_options(-fsanitize=memory -fPIE -pie)

add_compile_options(-fsanitize=undefined)
add_link_options(-fsanitize=undefined)

add_compile_options(-fsanitize=nullability)
add_link_options(-fsanitize=nullability)

add_compile_options(-fsanitize=implicit-conversion)
add_link_options(-fsanitize=implicit-conversion)

add_compile_options(-fsanitize=integer)
add_link_options(-fsanitize=integer)
add_compile_options(-fsanitize=local-bounds)
add_link_options(-fsanitize=local-bounds)
add_compile_options(-fsanitize=float-divide-by-zero)
add_link_options(-fsanitize=float-divide-by-zero)
#add_compile_options(-fsanitize=thread)
#add_link_options(-fsanitize=thread)

# package information
set(PACKAGE_NAME      "thealgos")
if (NOT DEFINED PACKAGE_VERSION)
  set(PACKAGE_VERSION   "0.0.1-dev")
endif()
set(PACKAGE_STRING    "${PACKAGE_NAME} ${PACKAGE_VERSION}")
set(PACKAGE_TARNAME   "${PACKAGE_NAME}-${PACKAGE_VERSION}")


include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/refs/tags/v1.14.0.zip
)
FetchContent_MakeAvailable(googletest)

set(CMAKE_POSITION_INDEPENDENT_CODE ON)

enable_testing()

add_executable(
  main_test
  main_test.cpp
)

target_link_libraries(
    main_test
  GTest::gtest_main
)

include(GoogleTest)
gtest_discover_tests(main_test)