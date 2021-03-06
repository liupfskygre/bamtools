# ==========================
# BamTools CMakeLists.txt
# (c) 2010 Derek Barnett
#
# src/toolkit
# ==========================

# set include path
include_directories( ${BamTools_SOURCE_DIR}/src/api
                     ${BamTools_SOURCE_DIR}/src/utils
                     ${BamTools_SOURCE_DIR}/src/third_party
                   )

# compile main bamtools application
add_executable( bamtools_cmd
                bamtools_convert.cpp
                bamtools_count.cpp
                bamtools_coverage.cpp
                bamtools_filter.cpp
                bamtools_header.cpp
                bamtools_index.cpp
                bamtools_merge.cpp
                bamtools_random.cpp
                bamtools_resolve.cpp
                bamtools_revert.cpp
                bamtools_sort.cpp
                bamtools_split.cpp
                bamtools_stats.cpp
                bamtools.cpp
              )

# set BamTools application properties
set_target_properties( bamtools_cmd PROPERTIES
                       OUTPUT_NAME "bamtools"
                     )
# make version info available in application
configure_file( ${CMAKE_CURRENT_SOURCE_DIR}/bamtools_version.h.in ${CMAKE_CURRENT_BINARY_DIR}/bamtools_version.h )
include_directories( ${CMAKE_CURRENT_BINARY_DIR} )

# set include paths for system JsonCpp
target_include_directories( bamtools_cmd PRIVATE ${JSONCPP_INCLUDE_DIRS} )

# define libraries to link
target_link_libraries( bamtools_cmd BamTools BamTools-utils ${JSONCPP_LDFLAGS} )

# set application install destinations
install( TARGETS bamtools_cmd DESTINATION "${CMAKE_INSTALL_BINDIR}" )
