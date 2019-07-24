if (NOT FIPS_IMPORT)
    cmake_minimum_required(VERSION 2.8)
    get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
    include("${FIPS_ROOT_DIR}/cmake/fips.cmake")
    
    set(FIPS_EXCEPTIONS ON CACHE BOOL "Enable C++ exceptions" FORCE)
    set(FIPS_RTTI  ON CACHE BOOL "Enable C++ RTTI" FORCE)

    fips_setup()
    fips_project(fips-openvdb)
endif()


list(APPEND CMAKE_MODULE_PATH "openvdb/cmake/")
fips_add_subdirectory(openvdb/)

fips_libs(openvdb_static Boost::iostreams Boost::system)


if (NOT FIPS_IMPORT)
    fips_finish()
endif()