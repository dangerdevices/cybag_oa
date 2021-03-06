# CMake 3.4.3 required to export all symbols on windows.
cmake_minimum_required(VERSION 3.4.3)

project(bagoa)

# organize targets into folders.
set_property(GLOBAL PROPERTY USE_FOLDERS ON)
# automatically export all DLL symbols on windows.
set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)

# set build configuration for make
set(CMAKE_BUILD_TYPE Release)

# set platform dependent compilation options
if (UNIX)
  message(status "** Setting GCC flags")
  # -fexceptions : enable exception handling
  # -g : include symbol information in executable for debugging.
  # -Wall : enable all warnings
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fexceptions -g -Wall -Wno-unused-variable")
else()
  message(status "** Setting MSVC flags")
  # s flag: enable C++ exceptions handling
  # c flag: functions declared as extern "C" will never throw C++ exception.
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /EHsc")
endif()

message(status "** CMAKE_CXX_FLAGS: ${CMAKE_CXX_FLAGS}")

add_subdirectory(src lib)
add_subdirectory(test bin)
