cmake_minimum_required (VERSION 3.5 FATAL_ERROR)

    # set the project name
    set (PROJECT_NAME             Library)

    # setup the type of output build Debug/Release
    set (CMAKE_BUILD_TYPE           Debug)

    # CMake standard variable names are long, I use something like aliases
    set (MAJOR      "${PROJECT_NAME}_VERSION_MAJOR")
    set (MINOR      "${PROJECT_NAME}_VERSION_MINOR")
    set (PATCH      "${PROJECT_NAME}_VERSION_PATCH")
    set (TWEAK      "${PROJECT_NAME}_VERSION_TWEAK")
    set (VERSION    "${PROJECT_NAME}_VERSION")

    # specify version number
    set (${MAJOR}   1)
    set (${MINOR}   0)
    set (${PATCH}   0)
    set (${TWEAK}   0)

    set (${VERSION}
            "${MAJOR}"."${MINOR}"."${PATCH}"."${TWEAK}"
    )

    # set the project name and version
    project (${PROJECT_NAME}
             ${VERSION}
             LANGUAGES CXX
    )   

    # specify the requirements of C++ standard
    set (CMAKE_CXX_STANDARD            17)
    set (CMAKE_CXX_STANDARD_REQUIRED True)

    # setup all warnings (Wall) 
    # setup optimization level (O2)
    add_definitions (-Wall -O2)
    
    set (OUTPUT_DIRECTORY  "${CMAKE_BINARY_DIR}")



    # find and gather all files by regix
    # NOTE: in case of use in Qt Creator we have to add header files :important
    file (GLOB
            CPP_SOURCES "${PROJECT_NAME}/src/*.cpp"
            PRV_HEADERS "${PROJECT_NAME}/inc/private/*.h"
            PUB_HEADERS "${PROJECT_NAME}/inc/*.h"
    )

# automatic creation of header files using CMake to pass version number and path
# configure_file (path.h.in          path.h)
# configure_file (version.h.in    version.h)

configure_file (
    "${PROJECT_SOURCE_DIR}/inc/path.h.in path.h"
    "${PROJECT_BINARY_DIR}/path.h"
) # Output: path.h
configure_file (
    "${PROJECT_SOURCE_DIR}/inc/version.h.in version.h"
    "${PROJECT_BINARY_DIR}/version.h"
) # Output: version.h


    # add directories were placed of the source files
    # NOTE: if we include directories no need to use PATH in sources
    include_directories ("${PROJECT_SOURCE_DIR}/src")
    include_directories ("${PROJECT_SOURCE_DIR}/inc/private")
    include_directories ("${PROJECT_SOURCE_DIR}/inc")

    # set the files to be connected to the target
    # add_executable (${PROJECT_NAME} main.cpp)
    # add_executable (${PROJECT_NAME} ${SOURCES})
    # or
    add_executable (${PROJECT_NAME}
                    ${CPP_SOURCES}
                    ${PRV_HEADERS}
                    ${PUB_HEADERS}
    )


# add directory to the list of paths to search for include files
target_include_directories (
        ${PROJECT_NAME}
    PUBLIC
        "${PROJECT_BINARY_DIR}"
)