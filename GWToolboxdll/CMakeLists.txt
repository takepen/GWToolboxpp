add_library(GWToolboxdll SHARED)

file(GLOB SOURCES
    "*.h"
    "*.cpp"
    "*.cc"
    "GWToolbox.rc"
    "Modules/*.h"
    "Modules/*.cpp"
    "Utils/*.h"
    "Utils/*.cpp"
    "Widgets/*.h"
    "Widgets/*.cpp"
    "Widgets/Minimap/*.h"
    "Widgets/Minimap/*.cpp"
    "Windows/*.h"
    "Windows/*.cpp")
source_group(TREE "${CMAKE_CURRENT_SOURCE_DIR}" FILES ${SOURCES})
target_sources(GWToolboxdll PRIVATE ${SOURCES})
target_precompile_headers(GWToolboxdll PRIVATE "stdafx.h")
target_compile_definitions(GWToolboxdll PRIVATE "_USRDLL")
target_compile_options(GWToolboxdll PRIVATE /W4 /WX /ZI)


target_include_directories(GWToolboxdll PRIVATE 
    "${CMAKE_CURRENT_SOURCE_DIR}"
    )

include(json)
include(imgui_fonts)
include(earcut)

target_link_libraries(GWToolboxdll PRIVATE
    # cmake targets:
    imgui
    gwca
    directx
	earcut
    utf8proc
    easywsclient
    discord_game_sdk
    nlohmann_json::nlohmann_json
    simpleini
    imgui::fonts
    IconFontCppHeaders
    # libs:
    Urlmon.lib
    Shlwapi.lib
    Wininet.lib
    Dbghelp.lib # for MiniDump
    xinput9_1_0.lib # for Win7 legacy support
    )
