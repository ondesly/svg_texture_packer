#
#  CMakeLists.txt
#  svg_rasterizer
#
#  Created by Dmitrii Torkhov <dmitriitorkhov@gmail.com> on 19.10.2020.
#  Copyright © 2020-2021 Dmitrii Torkhov. All rights reserved.
#

add_library(svg STATIC
    svg/rasterizer.cpp
    svg/renderer.cpp
)

target_link_libraries(svg PRIVATE cairo pugixml numerals)

set_target_properties(svg PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED YES
    CXX_EXTENSIONS NO)

target_include_directories(svg PRIVATE
    ${STB_INCLUDE_DIRS}

    ../include)

#

set(PUBLIC_HEADERS 
    ../include/svg/rasterizer.h
    ../include/svg/renderer.h)

install(TARGETS svg cairo pixman
        EXPORT svg-config
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION bin
        INCLUDES DESTINATION include)

install(FILES ${PUBLIC_HEADERS} DESTINATION include/svg)

install(EXPORT svg-config DESTINATION lib/cmake/svg)