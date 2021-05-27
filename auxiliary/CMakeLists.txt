include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_library(wauxlib STATIC
    denoise.c
    waux.c
    waux.h
    )

target_link_libraries(wauxlib wavelib)

set_property(TARGET wauxlib PROPERTY FOLDER "lib")

target_include_directories(wauxlib PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})

install(TARGETS wauxlib
    EXPORT wavelib-targets
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
