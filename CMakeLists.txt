cmake_minimum_required(VERSION 3.23)
project(fb2k_discord
        VERSION 1.0
        DESCRIPTION "Outputs Foobar now playing status to Discord"
        LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)

set(FB2K_SDK_PATH "${CMAKE_CURRENT_SOURCE_DIR}/libs/foobar/"  CACHE PATH "Path to foobar2000 SDK" FORCE)
set(DISCORD_SDK_PATH "${CMAKE_CURRENT_SOURCE_DIR}/libs/discord/" CACHE PATH "Path to Discord SDK" FORCE)

add_subdirectory(libs/foobar)

add_library(fb2k_discord SHARED
        main.cpp)

target_include_directories(fb2k_discord PRIVATE
        )

target_link_libraries(fb2k_discord
        pfc
        foobar2000_SDK
        foobar2000_component_client
        foobar2000_shared)

# Foobar component must have a name of `foo_` else it will not be loaded
set_target_properties(fb2k_discord PROPERTIES
        OUTPUT_NAME foo_discord_activity)