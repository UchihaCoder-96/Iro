find_package(glfw3 CONFIG REQUIRED)
find_package(glm CONFIG REQUIRED)
find_package(Vulkan REQUIRED)
find_program(GLSLC glslc REQUIRED)

add_library(Iro STATIC
    "src/Iro.cpp"
)

target_include_directories(Iro PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include")
set_property(TARGET Iro PROPERTY CXX_STANDARD 20)

target_link_libraries(Iro PUBLIC
    glfw
    glm::glm
    Vulkan::Vulkan
)

file(GLOB SHADERS "${CMAKE_CURRENT_SOURCE_DIR}/shaders/*.vert" "${CMAKE_CURRENT_SOURCE_DIR}/shaders/*.frag")
foreach(SHADER ${SHADERS})
    get_filename_component(NAME ${SHADER} NAME)
    set(SPIRV "${CMAKE_CURRENT_BINARY_DIR}/shaders/${NAME}.spv")
    add_custom_command(
        OUTPUT ${SPIRV}
        COMMAND ${GLSLC} ${SHADER} -o ${SPIRV}
        DEPENDS ${SHADER}
    )
    list(APPEND SPIRV_BINARY_FILES ${SPIRV})
endforeach()
add_custom_target(Shaders DEPENDS ${SPIRV_BINARY_FILES})
add_dependencies(Iro Shaders)

