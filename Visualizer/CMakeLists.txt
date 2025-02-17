cmake_minimum_required(VERSION 3.10)

project(ClearanceFieldVisualizer)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_EXPORT_COMPILE_COMMANDS 1)

# windows 动态库导出lib文件
set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)

# 设置VisualStudio使用utf-8编码
add_compile_options("$<$<C_COMPILER_ID:MSVC>:/utf-8>")
add_compile_options("$<$<CXX_COMPILER_ID:MSVC>:/utf-8>")


file(GLOB SOURCES *.cpp ../Source/*.cpp)
add_executable(ClearanceFieldVisualizer ${SOURCES})

find_package(argparse CONFIG REQUIRED)
find_package(spdlog CONFIG REQUIRED)
find_package(SDL2 CONFIG REQUIRED)
find_package(SDL2_ttf CONFIG REQUIRED)

include_directories("../Source")

target_link_libraries(ClearanceFieldVisualizer PRIVATE argparse::argparse)
target_link_libraries(ClearanceFieldVisualizer PRIVATE spdlog::spdlog)
target_link_libraries(ClearanceFieldVisualizer
    PRIVATE
    $<TARGET_NAME_IF_EXISTS:SDL2::SDL2main>
    $<IF:$<TARGET_EXISTS:SDL2::SDL2>,SDL2::SDL2,SDL2::SDL2-static>
)
target_link_libraries(ClearanceFieldVisualizer PRIVATE $<IF:$<TARGET_EXISTS:SDL2_ttf::SDL2_ttf>,SDL2_ttf::SDL2_ttf,SDL2_ttf::SDL2_ttf-static>)
