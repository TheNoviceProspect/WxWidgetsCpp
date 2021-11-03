cmake_minimum_required(VERSION 3.18.0)


#include(CTest)
#enable_testing()

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Move The Default Directory Of The Executable To bin Directory
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/bin)

file(TO_CMAKE_PATH "C:/Users/smzb_code/AppData/Local/Microsoft/Linux/HeaderCache/1.0/-114093420/usr/include" WININCLUDES)
file(TO_CMAKE_PATH "/usr/include" NIXINCLUDES)

# You can figure out what libraries you need here;
# https://www.wxwidgets.org/manuals/2.8/wx_librarieslist.html
# We need the Find package for wxWidgets to work
# NOTE: if you're using aui, include aui in this required components list.
#file(TO_CMAKE_PATH "C:/Users/smzb_code/Source/repos/apps/vcpkg/scripts/buildsystems" VCPKG_PATH)
#set(CMAKE_TOOLCHAIN_FILE ${VCPKG_PATH}"/vcpkg.cmake")
#  use : -DCMAKE_TOOLCHAIN_FILE="C:/Users/smzb_code/Source/repos/apps/vcpkg/scripts/buildsystems/vcpkg.cmake"
# It is essential that 'core' is mentioned before 'base'.

find_package(wxWidgets REQUIRED)

# wxWidgets include (this will do all the magic to configure everything)
include("${wxWidgets_USE_FILE}")


set(SOURCES_CXX_FILES
    "src/main.cpp"
)
set(HEADERS
    "include/main.hpp"
)

if(${CMAKE_SYSTEM_NAME} STREQUAL "Linux")
    add_executable(${PROJECT_NAME} ${SOURCES_CXX_FILES} ${HEADERS})
elseif(${CMAKE_SYSTEM_NAME} STREQUAL "Windows")
    add_executable(${PROJECT_NAME} WIN32 ${SOURCES_CXX_FILES} ${HEADERS})
endif()

include_directories(${CMAKE_BINARY_DIR}/dist/include)
target_include_directories(${PROJECT_NAME} PRIVATE ${wxWidgets_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} PRIVATE ${wxWidgets_LIBRARIES})

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)

####

#find_package(wxWidgets REQUIRED)
#target_include_directories(main PRIVATE ${wxWidgets_INCLUDE_DIRS})
#target_link_libraries(main PRIVATE ${wxWidgets_LIBRARIES})