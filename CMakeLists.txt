cmake_minimum_required(VERSION 3.16)

project(sfml-book)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

#===========================================================
# Đường dẫn tới SFML 2.6.2
#===========================================================

set(SFML_DIR "E:/SFML-2.6.2/lib/cmake/SFML")

find_package(SFML 2.6 REQUIRED COMPONENTS
    graphics
    window
    system
    audio
)

#===========================================================
# Hàm build chapter
#===========================================================

function(build_chapter TARGET)

    set(options)
    set(oneValueArgs)
    set(multiValueArgs SOURCES)

    cmake_parse_arguments(CHAPTER
        "${options}"
        "${oneValueArgs}"
        "${multiValueArgs}"
        ${ARGN}
    )

    include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../Include)

    add_executable(${TARGET}
        Main.cpp
        ${CHAPTER_SOURCES}
    )

    target_link_libraries(${TARGET}
        sfml-graphics
        sfml-window
        sfml-system
        sfml-audio
    )

endfunction()

#===========================================================
# Build các chapter
#===========================================================

add_subdirectory(01_Intro/Source)
add_subdirectory(02_Resources/Source)
add_subdirectory(03_World/Source)
add_subdirectory(04_Input/Source)
add_subdirectory(05_States/Source)