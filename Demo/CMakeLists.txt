add_executable(IroDemo main.cpp)
target_link_libraries(IroDemo PRIVATE Iro)
set_property(TARGET IroDemo PROPERTY CXX_STANDARD 20)

