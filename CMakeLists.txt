cmake_minimum_required(VERSION 3.16)

project(LA16 LANGUAGES C)

include(FetchContent)

FetchContent_Declare(
    lautils
    GIT_REPOSITORY https://github.com/lightweight-architecture/lautils.git
    GIT_TAG main
)

FetchContent_MakeAvailable(lautils)

add_executable(la16
    src/main.c

    src/core.c
    src/machine.c
    src/memory.c
    src/register.c

    src/instruction/arithmetic.c
    src/instruction/cmc.c
    src/instruction/core.c
    src/instruction/data.c
    src/instruction/execution.c
    src/instruction/ic.c
    src/instruction/ktrr.c
    src/instruction/mpp.c
)

target_include_directories(la16
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/include
)

target_link_libraries(la16
    PRIVATE lautils
)

add_library(la16_headers INTERFACE)

target_include_directories(la16_headers
    INTERFACE
        ${CMAKE_CURRENT_SOURCE_DIR}/include
)

target_compile_features(la16 PRIVATE c_std_99)
