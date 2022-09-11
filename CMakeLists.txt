cmake_minimum_required(VERSION 3.23)
project(fb2k_discord
        VERSION 1.0
        DESCRIPTION "Outputs Foobar now playing status to Discord"
        LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 14)

set(FB2K_SDK_PATH "${CMAKE_CURRENT_SOURCE_DIR}/libs/foobar/"  CACHE PATH "Path to foobar2000 SDK" FORCE)
set(DISCORD_SDK_PATH "${CMAKE_CURRENT_SOURCE_DIR}/libs/discord/" CACHE PATH "Path to Discord SDK" FORCE)

add_subdirectory(libs/foobar)
# This should work, although is likely not necessary?
#[[
include_external_msproject(fb2k_sdk ${FB2K_SDK_PATH}/foobar2000/SDK/foobar2000_SDK.vcxproj)
include_external_msproject(fb2k_sdk_helpers ${FB2K_SDK_PATH}/foobar2000/helpers/foobar2000_sdk_helpers.vcxproj)
include_external_msproject(fb2k_atl_helpers ${FB2K_SDK_PATH}/foobar2000/ATLHelpers/foobar2000_ATL_helpers.vcxproj)
include_external_msproject(fb2k_component_client ${FB2K_SDK_PATH}/foobar2000/foobar2000_component_client/foobar2000_component_client.vcxproj)
include_external_msproject(pfc ${FB2K_SDK_PATH}/pfc/pfc.vcxproj)
]]

add_library(fb2k_discord SHARED
        main.cpp)

target_include_directories(fb2k_discord PRIVATE
        ${FB2K_SDK_PATH}/foobar2000/SDK
        ${FB2K_SDK_PATH}/foobar2000/ATLHelpers
        ${FB2K_SDK_PATH}/foobar2000/shared
        ${FB2K_SDK_PATH}/foobar2000)

target_link_libraries(fb2k_discord
        pfc
        foobar2000_SDK
        foobar2000_component_client
        foobar2000_shared)
#[[
add_dependencies(fb2k_discord
        fb2k_sdk
        fb2k_sdk_helpers
        fb2k_atl_helpers
        fb2k_component_client
        pfc)

target_link_libraries(fb2k_discord
        ${FB2K_SDK_PATH}/foobar2000/shared/shared-Win32.lib)]]
