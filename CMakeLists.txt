cmake_minimum_required(VERSION "3.16")

project("Assessment")
add_subdirectory(test)
include(FetchContent)
FetchContent_Declare(
  googletest
  # Specify the commit you depend on and update it regularly.
  URL https://github.com/google/googletest/archive/609281088cfefc76f9d0ce82e1ff6c30cc3591e5.zip
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)
include_directories(${PROJECT_SOURCE_DIR})
add_executable("${PROJECT_NAME}" main.cpp  day1.cpp StringHelper.cpp FileLoader.cpp)
target_link_libraries("${PROJECT_NAME}" gtest_main)
add_test(NAME mytest COMMAND "${PROJECT_NAME}")
