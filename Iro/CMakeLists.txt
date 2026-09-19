# CMake project for Iro

find_package(glfw3 CONFIG REQUIRED)
find_package(glm CONFIG REQUIRED)
find_package(Vulkan REQUIRED)

add_executable(Iro
    "Iro.cpp"
    "Iro.h"
)

if (CMAKE_VERSION VERSION_GREATER 3.12)
    set_property(TARGET Iro PROPERTY CXX_STANDARD 20)
endif()

target_link_libraries(Iro PRIVATE
    glfw
    glm::glm
    Vulkan::Vulkan
)

