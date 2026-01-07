cmake_minimum_required(VERSION 3.16)
project(SDL2_ImGui_App LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# ---------------- ImGui ----------------
set(IMGUI_DIR ${CMAKE_SOURCE_DIR}/imgui)

set(IMGUI_SOURCES
    ${IMGUI_DIR}/imgui.cpp
    ${IMGUI_DIR}/imgui_draw.cpp
    ${IMGUI_DIR}/imgui_tables.cpp
    ${IMGUI_DIR}/imgui_widgets.cpp
    ${IMGUI_DIR}/backends/imgui_impl_sdl2.cpp
    ${IMGUI_DIR}/backends/imgui_impl_opengl3.cpp
)

# ---------------- Executable ----------------
add_executable(app
    main.cpp
    ${IMGUI_SOURCES}
)

# ---------------- Includes ----------------
target_include_directories(app PRIVATE
    ${IMGUI_DIR}
    ${IMGUI_DIR}/backends
    C:/msys64/mingw64/include/SDL2   # MSYS2 SDL2 include
)

# ---------------- Libraries ----------------
target_link_libraries(app PRIVATE
    C:/msys64/mingw64/lib/libSDL2.a  # SDL2
    opengl32                          # OpenGL
    setupapi                          # SetupAPI functions (HID)
    imm32                             # IME/keyboard
    winmm                             # timers & audio
    version                           # version info
    cfgmgr32                           # CM_* device functions
)

# ---------------- Windows settings ----------------
if (WIN32)
    target_compile_definitions(app PRIVATE SDL_MAIN_HANDLED)
endif()