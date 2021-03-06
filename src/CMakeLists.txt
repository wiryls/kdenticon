# set the target name
set(name "kdenticon")

# collect all header files and source files
file(GLOB_RECURSE headers CONFIGURE_DEPENDS "${PROJECT_SOURCE_DIR}/include/*.hpp")
set(sources "")

# build as a library
add_library(${name} INTERFACE ${sources} ${headers})

# target options
source_group              (TREE "${PROJECT_SOURCE_DIR}" FILES ${sources} ${headers})
set_target_properties     (${name} PROPERTIES FOLDER "${PROJECT_NAME}")
set_target_properties     (${name} PROPERTIES CXX_STANDARD 17)
target_include_directories(${name} INTERFACE "${PROJECT_SOURCE_DIR}/include")
target_link_libraries     (${name} INTERFACE "")
target_compile_options    (${name} INTERFACE
    "$<$<NOT:$<CXX_COMPILER_ID:MSVC>>:-pedantic-errors;-Wall;-Wextra;-Wconversion;-Werror>"
    "$<$<AND:$<CONFIG:RELEASE>,$<NOT:$<CXX_COMPILER_ID:MSVC>>>:-O3>"
    "$<$<AND:$<CONFIG:DEBUG>,$<NOT:$<CXX_COMPILER_ID:MSVC>>>:-g>"

    "$<$<CXX_COMPILER_ID:MSVC>:/WX;/W4;/utf-8>"
    "$<$<AND:$<CONFIG:RELEASE>,$<CXX_COMPILER_ID:MSVC>>:/O2>")
