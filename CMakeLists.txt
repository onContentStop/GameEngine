cmake_minimum_required(VERSION 3.0.0)
project(game-engine VERSION 0.1.0)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

include(CTest)
enable_testing()

file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS "src/*.cpp")
file(GLOB_RECURSE HEADERS "src/*.hpp")

add_library(game-engine ${SOURCES} ${HEADERS})

find_package(SDL2 CONFIG REQUIRED)
find_package(sdl2-image CONFIG REQUIRED)
find_package(sdl2-gfx CONFIG REQUIRED)
find_package(fmt CONFIG REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC SDL2::SDL2main SDL2::SDL2-static SDL2::SDL2_gfx SDL2::SDL2_image fmt::fmt)
target_include_directories(${PROJECT_NAME} PUBLIC "${PROJECT_SOURCE_DIR}/src")
set_target_properties(${PROJECT_NAME} PROPERTIES PUBLIC_HEADER "${HEADERS}")
message("Headers: ${HEADERS}")

install(TARGETS ${PROJECT_NAME} 
        PUBLIC_HEADER DESTINATION include/GameEngine
        LIBRARY DESTINATION lib
)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
