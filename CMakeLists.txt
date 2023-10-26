cmake_minimum_required (VERSION 3.0...3.27.4)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

if (CMAKE_BUILD_TYPE STREQUAL None)
    set(CMAKE_BUILD_TYPE RelWithDebInfo)
endif()

project (rockprog VERSION 0.1.0)
add_definitions(-DVERSION="${PROJECT_VERSION}-dev")

include(GNUInstallDirs)

find_package(PkgConfig REQUIRED)
pkg_check_modules(libusb REQUIRED libusb-1.0)
pkg_check_modules(libpopt REQUIRED popt)

add_executable(rockprog rockprog.c softrock.c)
target_link_libraries(rockprog ${libusb_LIBRARIES} ${libpopt_LIBRARIES})
target_include_directories(rockprog PUBLIC ${libusb_INCLUDE_DIRS} ${libpopt_INCLUDE_DIRS})
install(TARGETS rockprog DESTINATION ${CMAKE_INSTALL_BINDIR})
