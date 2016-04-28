cmake_minimum_required (VERSION 3.0 FATAL_ERROR)
project (py-leveldb)

find_package(leveldb REQUIRED)
include_directories(${leveldb_INCLUDE_DIRS})

## include & link PythonLibs
find_package(PythonLibs 2 REQUIRED)
include_directories(${PYTHON_INCLUDE_DIRS})
link_libraries(${PYTHON_LIBRARIES})

# Add files :
file(GLOB SRC_FILES "*.cc")
file(GLOB INC_FILES "*.h")
file(GLOB DEF_FILES "*.def")

message("Source .cc files : ${SRC_FILES}")
message("Source .h files : ${INC_FILES}")
message("Source .def files : ${DEF_FILES}")

add_definitions("-DDLL_BUILD")
add_library(pyleveldb MODULE ${SRC_FILES} ${INC_FILES} ${DEF_FILES})
set_target_properties(pyleveldb PROPERTIES SUFFIX ".pyd"
                                           OUTPUT_NAME leveldb)
                                           
target_link_libraries(pyleveldb ${leveldb_LIBRARIES})
	
install(TARGETS pyleveldb DESTINATION bin)

include(TargetCopyDependencies.cmake)
target_copy_dependencies(pyleveldb
                         # we know dependencies are one level up
                         DEPENDENCIES_DIR ${CMAKE_INSTALL_PREFIX}/..
                         # copy to install dir   
                         DESTINATION "${CMAKE_INSTALL_PREFIX}/bin"
                         # use hard links
                         USE_HARD_LINKS
                         )

# TODO add test


