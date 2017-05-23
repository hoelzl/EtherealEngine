cmake_minimum_required(VERSION 3.7)

project (ethereal)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

if(UNIX AND NOT APPLE)
    set(LINUX TRUE)
endif()

# if(NOT LINUX) should work, too, if you need that
if(LINUX)
    message(STATUS "OS >>> Linux")
    # linux stuff here
elseif(WIN32)
    message(STATUS "OS >>> Windows")
    # stuff that should happen not on Linux
endif()

message(STATUS "COMPILER >>> ${CMAKE_CXX_COMPILER_ID}")

option(BUILD_SHARED_LIBS
  "Build package with shared libraries."
  OFF
)
message(STATUS "BUILD_SHARED_LIBS >>> ${BUILD_SHARED_LIBS}")

add_definitions(-DPROJECT_DIRECTORY="${PROJECT_SOURCE_DIR}")

function(add_subdirectory_ex arg1)
	message(STATUS "---------Configure ${arg1}")
	add_subdirectory(${arg1})
	message(STATUS "---------Done ${arg1}")
endfunction(add_subdirectory_ex)

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin) 
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib) 

if(MSVC)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /MP /bigobj")
endif()
message(STATUS "CMAKE_CXX_FLAGS >>> ${CMAKE_CXX_FLAGS}")
message(STATUS "CMAKE_CXX_FLAGS_DEBUG >>> ${CMAKE_CXX_FLAGS_DEBUG}")
message(STATUS "CMAKE_CXX_FLAGS_RELEASE >>> ${CMAKE_CXX_FLAGS_RELEASE}")

add_subdirectory_ex(engine)
add_subdirectory_ex(editor)
add_subdirectory_ex(3rdparty)