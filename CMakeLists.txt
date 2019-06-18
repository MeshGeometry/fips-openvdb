if (NOT FIPS_IMPORT)
    cmake_minimum_required(VERSION 2.8)
    get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
    include("${FIPS_ROOT_DIR}/cmake/fips.cmake")
    
    set(FIPS_EXCEPTIONS ON CACHE BOOL "Enable C++ exceptions" FORCE)
    set(FIPS_RTTI  ON CACHE BOOL "Enable C++ RTTI" FORCE)

    fips_setup()
    fips_project(fips-openvdb)
endif()


list(APPEND CMAKE_MODULE_PATH "${FIPS_PROJECT_DIR}/openvdb/cmake/")

#set(OPENVDB_ROOT ${FIPS_PROJECT_DIR}/openvdb)
#set(OPENVDB_LIBRARYDIR lib/cmake/OpenVDB)
#set(OpenVDB_INCLUDE_DIR openvdb/openvdb)
#set(OpenVDB_LIB_COMPONENTS TBB)
#find_package(OpenVDB 6.1.1 EXACT REQUIRED COMPONENTS TBB)

#find_package(TBB Reuired)
#install(FILES FindTBB.cmake DESTINATION lib/cmake/OpenVDB)

#if (NOT OpenVDB_FOUND)
#    message(FATAL_ERROR "OpenVDB SDK not found!")
#endif()

#fips_include_directories(${FIPS_PROJECT_DIR}/openvdb)
fips_add_subdirectory(${FIPS_PROJECT_DIR}/openvdb)
fips_libs(openvdb_static)


if (NOT FIPS_IMPORT)
    fips_finish()
endif()