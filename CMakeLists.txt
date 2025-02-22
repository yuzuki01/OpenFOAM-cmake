cmake_minimum_required(VERSION 3.20)
project(icoFoam)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(DEFINITIONS_COMPILE
        "-std=c++11 -m64 -Dlinux64 -DWM_ARCH_OPTION=64 -DWM_DP -DWM_LABEL_SIZE=32 -Wall -Wextra \
        -Wnon-virtual-dtor -Wno-unused-parameter -Wno-invalid-offsetof -Wno-attributes -O3  -DNoRepository \
        -ftemplate-depth-100  -fPIC -Wno-unused-variable -Wno-old-style-cast $ENV{PFLAGS} $ENV{PINC}"
)
add_definitions("${DEFINITIONS_COMPILE}")

if (DEFINED ENV{WM_PROJECT})
    message(STATUS "${PROJECT_NAME} using $ENV{WM_PROJECT}-$ENV{WM_PROJECT_VERSION}")
    set(WM_PATH, ${CMAKE_SOURCE_DIR})
else ()
    message(FATAL_ERROR "OpenFOAM environment not set. Aborting.")
endif ()
# OpenFOAM include
include_directories(.
        "$ENV{FOAM_SRC}/OpenFOAM/lnInclude"
        "$ENV{FOAM_SRC}/OSspecific/POSIX/lnInclude")

# Make/files
set(EXECUTABLE_OUTPUT_PATH "$ENV{FOAM_APPBIN}")  # $ENV{FOAM_USER_APPBIN}
set(LIBRARY_OUTPUT_PATH "$ENV{FOAM_LIBBIN}")     # $ENV{FOAM_USER_LIBBIN}
set(CMAKE_SHARED_LIBRARY_PREFIX "")

# Make/options
include_directories(
        "$ENV{FOAM_SRC}/finiteVolume/lnInclude"
        "$ENV{FOAM_SRC}/meshTools/lnInclude"
)

link_directories($ENV{FOAM_LIBBIN} $ENV{FOAM_LIBBIN}/dummy $ENV{FOAM_LIBBIN}/${PATH_LIB_OPENMPI})

add_executable(${PROJECT_NAME}
        icoFoam.C
)

# OpenFOAM lib
target_link_libraries(${PROJECT_NAME} OpenFOAM dl m Pstream fvOptions)

# Make/options
target_link_libraries(${PROJECT_NAME} finiteVolume meshTools)

# add_subdirectory(src/LIB_NAME)
# target_link_libraries(${PROJECT_NAME} LIB_NAME)

# check MPI
find_package(MPI REQUIRED)
if (MPI_FOUND)
    include_directories(${MPI_INCLUDE_PATH})
    target_link_libraries(${PROJECT_NAME} ${MPI_LIBRARIES})
endif ()
