include(FetchContent)
include(CMakePrintHelpers)

if(NOT TARGET imgui)
    # Fetch dependencies (modern CMake approach)
    include(FetchContent)

    # Dear ImGui
    FetchContent_Declare(
        imgui
        GIT_REPOSITORY https://github.com/ocornut/imgui.git
        GIT_TAG v1.92.0-docking
    )
    FetchContent_MakeAvailable(imgui)

    # OpenGL (system library)
    find_package(OpenGL REQUIRED)

    # Configure ImGui with GLFW + OpenGL3 backend
    set(IMGUI_DIR ${imgui_SOURCE_DIR})
    file(GLOB IMGUI_SOURCES
        "${IMGUI_DIR}/*.cpp"
    )
    add_library(imgui STATIC ${IMGUI_SOURCES})

    target_include_directories(imgui PUBLIC
    ${IMGUI_DIR}
    ${glfw_SOURCE_DIR}/include
    )
endif()
