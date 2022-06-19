cmake_minimum_required ( VERSION 3.20 )

project ( testprj )

set ( PRJ_INCLUDE_DIRS )
set ( PRJ_COMPILE_FEATURES )
set ( PRJ_LIBRARIES )

list ( APPEND PRJ_COMPILE_FEATURES cxx_std_20 )

#CGAL_Qt5 is needed for the drawing.
find_package(CGAL REQUIRED OPTIONAL_COMPONENTS Qt5)
create_single_source_cgal_program("sm_derivation.cpp")
create_single_source_cgal_program("sm_join.cpp")
create_single_source_cgal_program("sm_aabbtree.cpp")
create_single_source_cgal_program("sm_bgl.cpp")
create_single_source_cgal_program("sm_circulators.cpp")
create_single_source_cgal_program("sm_do_intersect.cpp")
create_single_source_cgal_program("sm_iterators.cpp")
create_single_source_cgal_program("sm_kruskal.cpp")
create_single_source_cgal_program("sm_memory.cpp")
create_single_source_cgal_program("sm_properties.cpp")
create_single_source_cgal_program("sm_draw_small_faces.cpp")
create_single_source_cgal_program("check_orientation.cpp")
#create the executable of the application
create_single_source_cgal_program("draw_surface_mesh.cpp")

message ( STATUS "CGAL_Qt5_FOUND    = ${CGAL_Qt5_FOUND}" )

if(CGAL_Qt5_FOUND)
  #link it with the required CGAL libraries
  target_link_libraries(draw_surface_mesh PUBLIC CGAL::CGAL_Basic_viewer)
  target_link_libraries(sm_draw_small_faces PUBLIC CGAL::CGAL_Basic_viewer)
endif()

list ( APPEND PRJ_LIBRARIES CGAL::CGAL )
add_executable ( ${PROJECT_NAME}
    main.cpp
)

target_include_directories ( ${PROJECT_NAME}
    PRIVATE 
        ${PRJ_INCLUDE_DIRS}
)

target_link_libraries( ${PROJECT_NAME} 
    PRIVATE 
        ${PRJ_LIBRARIES}
)

target_compile_features ( ${PROJECT_NAME} 
    PRIVATE 
        ${PRJ_COMPILE_FEATURES}
)