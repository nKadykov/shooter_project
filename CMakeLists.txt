cmake_minimum_required(VERSION 3.10)
project(shooter_project)

set(CMAKE_TOOLCHAIN_FILE "C:/vcpkg/scripts/buildsystems/vcpkg.cmake")

set(CMAKE_CXX_STANDART 23)
set(CMAKE_CXX_STANDART_REQUIRED ON)

set(ASSETS_FOLDER ${CMAKE_SOURCE_DIR}/assets)
if(WIN32)
    set(ASSETS_OUTPUT_DIR Release/assets)
else()
    set(ASSETS_OUTPUT_DIR assets)
endif()

include_directories(include)

add_executable(shooter_project src/bullet.cpp src/button.cpp src/enemy.cpp src/game.cpp src/gameoverwindow.cpp src/healthbar.cpp src/healthpoint.cpp src/main.cpp src/menu.cpp src/player.cpp include/bullet.h include/button.h include/enemy.h include/game.h include/gameoverwindow.h include/healthbar.h include/healthpoint.h include/menu.h include/player.h)

find_package(SFML 2.5 COMPONENTS system window graphics network audio REQUIRED)
target_link_libraries(shooter_project sfml-system sfml-window sfml-graphics sfml-network sfml-audio)

add_custom_command(
    TARGET shooter_project POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
    ${ASSETS_FOLDER} ${ASSETS_OUTPUT_DIR}
    COMMENT "Copying assets to output directory"
)