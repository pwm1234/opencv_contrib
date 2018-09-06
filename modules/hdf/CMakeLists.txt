set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR})

if(NOT CMAKE_CROSSCOMPILING) # iOS build should not reuse OSX package
    find_package(HDF5)
endif()

if(NOT HDF5_FOUND)
    ocv_module_disable(hdf) # no return
endif()

set(HAVE_HDF5 1)

ocv_warnings_disable(CMAKE_CXX_FLAGS -Winvalid-offsetof)

set(the_description "Hierarchical Data Format I/O")
ocv_define_module(hdf opencv_core WRAP python)
ocv_target_link_libraries(${the_module} hdf5::hdf5-shared)
ocv_include_directories(${HDF5_INCLUDE_DIRS})
