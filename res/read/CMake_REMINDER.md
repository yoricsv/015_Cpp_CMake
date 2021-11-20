#  <p align=center> <b>Installing and using CMake</b></p> 


## [*CMake reference guide*](https://cmake.org/documentation) 

![cmakeContent][cmake]
[cmake]: res/img/

### Global variables 
```cmake
CMAKE_BINARY_DIR                # <-- build folder by default (contains cache, tests results etc.)./cmake-build-debug
CMAKE_SOURCE_DIR                # <-- folder where located root CMakeLists.txt file
CMAKE_CURRENT_SOURCE_DIR        # <-- folder where located current CMakeLists.txt file
```


## [*Download*][1] CMake from the official website

[1]: https://cmake.org/download/
---
<br/>
<br/>

##  <p align=center> <b>Installation on Linux</b></p>
---

*Find a place for unzipping and installing*
```bash
tar -zxvf cmake-3.14.5.tar.gz
```
```bash
cd cmake-3.14.5/
```
<br/>

*According to the README file, run the following command to install.*
```bash
./bootstrap && make && sudo make install
```

By default, CMake will be installed in */usr/local/bin*.
<br/>
<br/>

*Compile and Install CMake*
```bash
cd build/
```
```bash
cmake ..
```
```bash
make
```
```bash
sudo make install
```
---
<br/>
<br/>

##  <p align=center> <b>Creating and testing CMake</b></p>
---
<br/>
Create a new folder as your project folder, create a new CMakeLists.txt file

*Below is a typical configuration:*

```cmake
# Set minimum requirements for CMake version
# If your version isn't applicable - you'll get a notification 
CMAKE_MINIMUM_REQUIRED (VERSION 3.14)

# This defines the PROJECT_NAME and LANGUAGE
PROJECT (CMakeTest CXX)

# Add all source and header files from the src directory to the SRC_LIST variable
AUX_SOURCE_DIRECTORY (src
                        SRC_LIST
)

# Build the application HELLO
ADD_EXECUTABLE   (hello
                        ${SRC_LIST}
)
```
After adding the source code to * src *, create a build folder in the project root.
<br/>


*Then do:*
```bash
cd build/
```
```bash
cmake ..
```
```bash
make
```

The compiled and executable file *Hello* will be created in the *Build* directory.

```cmake
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib CACHE PATH "Where to place compiled static libraries.")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib CACHE PATH "Where to place compiled shared libraries.")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin CACHE PATH "Where to place compiled executables.")
```
---
<br/>
<br/>


##  <p align=center> <b>CMake for Visual Studio</b></p>

---
- Syntax CMake.
- Grammatical features
---
<br/>

*Assignment operator*

```cmake
# CACHE VARIABLES               (Access by: $CACHE{<var>})  
# (Global visibility, stored in CMakeCache.txt)
# (if ordinary variables with the same name are not defined
# - can be called by ${<var>})
set (<var>
        <value>
     CACHE
        <STRING | BOOL | FILEPATH | PATH>
     INTERNAL
)

# ENVIRONMENTAL VARIABLES       (Access by: $ENV{<var>})
# (Global visibility)
set (ENV
        {<var>}
        <path>
)

# PARENT SCOPE VARIABLES        (Access by: ${<var>})
# (doesn't affect to the environmental variables)
set (<var>
     <value>
     PARENT_SCOPE
)

# CHILD VARIABLES               (Access by: ${<var>})
# (doesn't affect to the parental variables)
# Can be used as an array - set (VAR a b c) 
# or LIST (set (VAR "a b c"))
set (<var>
     <value>
)

# DELETE VARIABLES
unset (<var> [CACHE | PARENT_SCOPE])
unset (ENV   {<variable>})
```

*Functions for working with the List*
```cmake
# Read values in the List
list (LENGTH
        <list>
        <out-var>
)
list (GET   
        <list>
        <element   index>
        [<index> ...]
        <out-var>
)
list (JOIN
        <list>
        <glue>
        <out-var>
)
list (SUBLIST
        <list>
        <begin>
        <length>
        <out-var>
)

# Search values in the List
list (FIND
        <list>
        <value>
        <out-var>
)

# Remove values from the List
list (APPEND
        <list>
        [<element>...]
)
list (FILTER   
        <list>
        {INCLUDE | EXCLUDE}
        REGEX
            <regex>
)
list (INSERT    
        <list>
        <index>
        [<element>...]
)
list (POP_BACK    
        <list>
        [<out-var>...]
)
list (POP_FRONT   
        <list>
        [<out-var>...]
)
list (PREPEND   
        <list>
        [<element>...]
)
list (REMOVE_ITEM   
        <list>
        <value>...
)
list (REMOVE_AT
        <list>
        <index>...
)
list (REMOVE_DUPLICATES 
        <list>
)
list (TRANSFORM
        <list>
        <ACTION>
        [...]
)

 # Sort values in the List
list (REVERSE    
        <list>
)
list (SORT    
        <list>
        [...]
)
```

*Conditional Operators*
```cmake
if (<condition>)
    <commands>
elseif (<condition>)
    <commands>
else ()
    <commands>
endif ()
```

*Functions*
```cmake
function (<func_name> [arg1 [arg2 [arg3 ...]]])
    <commands>
endfunction ()
 ```

*Macros*
```cmake
macro (<name> [arg1 [arg2 [arg3 ...]]])
    <commands>
endmacro ()
```

*Built-in functions*
```cmake
# Set minimum requirements for CMake version (at the beginning of the file)
# cmake_minimum_required (VERSION 3.14 FATAL_ERROR)
cmake_minimum_required (VERSION <min>[...<max>] [FATAL_ERROR])
```

*Define the project name*
```cmake
project (<project_name>)

# Добавить и построить подпроект (то есть папку, содержащую CMakeLists.txt)
add_subdirectory (<project_dir> 
                  [binary_dir]
                  [EXCLUDE_FROM_ALL]
)

# Добавить файлы c / cpp во всей папке в список исходных файлов,
# Получить строку типа "src / main.cpp; src / s.cpp; ..."
# aux_source_directory (src SRC_LIST)
aux_source_directory (<src_dir>
                      <source_list>
)

# Генерация исполняемых файлов на основе предоставленных параметров исходного файла
# add_executable (CMakeTest.exe ${SRC_LIST})
add_executable (<target_exe>
                [WIN32]
                [MACOSX_BUNDLE]
                [EXCLUDE_FROM_ALL]
                [source1]
                [source2 ...]
)

# То же, что и выше, сборка библиотеки
# add_library (Dependency.lib d1.cpp)
add_library (<target_lib>
            [STATIC | SHARED | MODULE]
            [EXCLUDE_FROM_ALL]
            [source1]
            [source2 ...]
)

# Добавить каталог заголовочных файлов (указать #include 
# "xxx.h" без добавления относительного пути)
# include_directories (Dependency)
include_directories ([AFTER|BEFORE]
                     [SYSTEM]
                     dir1
                     [dir2 ...]
)

# Добавить каталог заголовочных файлов к указанной цели
# target_include_directories (CMakeTest.exe PRIVATE Dependency)
target_include_directories (<target>
                            [SYSTEM]
                            [BEFORE]
                            <INTERFACE|PUBLIC|PRIVATE>
                            [items1...]
                            [
                                <INTERFACE|PUBLIC|PRIVATE>
                                [items2...] ...
                            ]
)

# Ссылка на ранее созданные исполняемые файлы и библиотеки
# target_link_libraries (CMakeTest.exe Dependency.lib)
target_link_libraries (<target>
                        ...
                       <item>
                       ...
                       ...
)
```
<br/>
<br/>

#  <p align=center> <i>Встроенные переменные</i></p>

**Variable** | **Description**
--- | ---
CMAKE_SOURCE_DIR<br/>PROJECT_SOURCE_DIR<br/> CMAKE_CURRENT_SOURCE_DIR <br/><PROJECT_NAME>_SOURCE_DIR<br/>| All points to the absolute path to the source directory of the project <br/>(CMakeLists.txt file location is absolute path).<br/>It might be different if the project will consist of several more projects.
CMAKE_SOURCE_DIR | Contains the path to the top level of root directory (CMakeLists.txt) for the current project <br/>(parent project).
PROJECT_SOURCE_DIR | This is the source directory of the last call to the project() command made in the current directory scope or one of its parents<br/> (subproject).
CMAKE_CURRENT_SOURCE_DIR | This the full path to the source directory that is currently being processed by CMakeLists.txt.
<PROJECT_NAME>_SOURCE_DIR | Define the path to the current CMakeLists.txt folder (don't define before call).
<br/>

Поэтому, когда нет подпроектов, они одинаковы.
Например, для родительского проекта Outer c подпроектом Inner:
```cmake
# Outer/CMakeLists.txt
...
         project (Outer)
add_subdirectory (Inner)
...
```
```cmake
# Outer/Inner/CMakeLists.txt
...
project (Inner)
...
```
<br/>

*В Outer/CMakeLists.txt переменные будут иметь следующие значения:*

**Variable** | **Value**
--- | ---
CMAKE_SOURCE_DIR | /. . ./Outer
PROJECT_SOURCE_DIR | /. . ./Outer
CMAKE_CURRENT_SOURCE_DIR | /. . ./Outer
Outer_SOURCE_DIR | /. . ./Outer
Inner_SOURCE_DIR | /. . ./Outer/Inner
<br/>
				
*В Outer/Inner/CMakeLists.txt переменные будут иметь следующие значения:*

**Variable** | **Value**
--- | ---
CMAKE_SOURCE_DIR | /.../Outer
PROJECT_SOURCE_DIR | /.../Outer/Inner
CMAKE_CURRENT_SOURCE_DIR | /.../Outer/Inner
Outer_SOURCE_DIR | /.../Outer
Inner_SOURCE_DIR | /.../Outer/Inner
<br/>

---

#  **TODO:**<br>*PROJECT_SOURCE_DIR* против <br/> *CMAKE_CURRENT_SOURCE_DIR* различия.



**Variable** | **Description**
--- | ---
CMAKE_BINARY_DIR<br/>PROJECT_BINARY_DIR<br/>CMAKE_CURRENT_BINARY_DIR<br/><PROJECT_NAME>_BINARY_DIR | Укажите абсолютный путь, по которому происходит компиляция проекта.<br/>Разница та же, что и выше.
<br/>

Если он скомпилирован в исходном коде, он ссылается на каталог верхнего уровня проекта, то есть <. . .>_SOURCE_DIR То же самое. 



``` cmake
cmake_minimum_required (VERSION 3.5 FATAL_ERROR)

    # set the product name
    set (PROJECT_NAME      ProjectName)

    set (OUTPUT_DIRECTORY  "${CMAKE_BINARY_DIR}")

    # setup version number
    set (PROJECT_VERSION_MAJOR 1)
    set (PROJECT_VERSION_MINOR 0)
    set (PROJECT_VERSION_PATCH 0)
    set (PROJECT_VERSION_TWEAK 0)

    # set the project name and version
project (${PROJECT_NAME}  VERSION 1.0.0.0 LANGUAGES CXX)

    # setup the type of output build Debug/Release
    # by default generates the Release version
    set (CMAKE_BUILD_TYPE Debug)


    # FLAGS
    
    # setup flag for using standard 
    # VALUES: c++03/c++11/c++14/c++17/c++19/c++1y
    #
    # set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17")
    # set (CMAKE_C_FLAGS   "${CMAKE_C_FLAGS}   -std=c11"  )
    # or
    # set (CMAKE_CXX_STANDARD 17)
    # set (CMAKE_C_STANDARD   11)
    
    add_definitions(-std=c++17)

    # setup all warnings (Wall) 
    # setup optimization level (O2)
    #
    # set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -O2")

    add_definitions (-Wall -O2)

    # set (SOURCES main.cpp)
    # or
    file (GLOB
            CPP    "*.cpp"
            CLANG  "*.c"  )
    
    # add_executable (${PROJECT_NAME} main.cpp)
    # add_executable (${PROJECT_NAME} ${SOURCES})
    # or
    add_executable (${PROJECT_NAME} ${CPPS} ${CLANG})






target_include_directories (${PROJECT_NAME} PUBLIC "${PROJECT_BINARY_DIR}")
```


```cmake
cmake_minimum_required(VERSION 3.5)

# ${PROJECT_NAME}
#set(PROJECT_NAME HW-015_CMake_HelloWorld)
project(HW-015_CMake_HelloWorld LANGUAGES CXX)

#set(CMAKE_BUILD_TYPE Debug)
set(CMAKE_BUILD_TYPE Release)

#set(CMAKE_CXX_STANDART 11)    # enable C++11 standard
#set(CMAKE_CXX_STANDART 14)    # enable C++11 standard
#set(CMAKE_CXX_STANDART 17)    # enable C++11 standard
#set(CMAKE_CXX_STANDART 1y)    # enable latest standard
# first one the same as next
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14")
#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17")
#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14")

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")

#set(SOURCES main.cpp)
# first one the same as next, but must to fill it manually 
file(GLOB CPPS "*.cpp")

add_executable(HW-015_CMake_HelloWorld main.cpp)
#add_executable(${PROJECT_NAME} main.cpp)
# or
#add_executable(${PROJECT_NAME} ${CPPS})

#add_executable(${PROJECT_NAME} ${SOURCES})
```


<!--  NEW -->
```cmake
cmake_minimum_required(VERSION 3.21)

    # set the project name
    set (PROJECT_NAME  HWRandNumber)

project( ${PROJECT_NAME}
         LANGUAGES
         CXX
)
    # automatically adds CMAKE_CURRENT_SOURCE_DIR and
    # CMAKE_CURRENT_BINARY_DIR to the include path
    # for each directory
    set(CMAKE_INCLUDE_CURRENT_DIR ON)

    # specify the requirements of C++ standard
    set(CMAKE_CXX_STANDARD          17)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)

    # setup all warnings (Wall) optimization level (O3)
    add_definitions (-Wall -O3)
    # or the same
#    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17 -Wall -O3")
    
    # specify where locate target builds
    set (OUTPUT_DIRECTORY  "${CMAKE_CURRENT_SOURCE_DIR}/build")

#    set(SOURCE_DIR "${PROJECT_SOURCE_DIR}/src")
#    aux_source_directory(${SOURCE_DIR} SRC_LIST)
    # find and gather all files by regix
    # NOTE: in case of use in Qt Creator we have to add header files :important
#    file (GLOB
#            CPP_SOURCES "${CMAKE_BINARY_DIR}/${PROJECT_NAME}/src/*.cpp"
#            PRV_HEADERS "${PROJECT_NAME}/inc/private/*.h"
#            PUB_HEADERS "${PROJECT_NAME}/inc/*.h"
#    )

    # add directories were placed of the source files
    # NOTE: if we include directories no need to use PATH in sources
#    include_directories ("${PROJECT_SOURCE_DIR}/src")
#    include_directories ("${PROJECT_SOURCE_DIR}/inc/private")
#    include_directories ("${PROJECT_SOURCE_DIR}/inc")

    # set the files to be connected to the target
    # add_executable (${PROJECT_NAME} main.cpp)
    # add_executable (${PROJECT_NAME} ${SOURCES})
    # or
    add_executable (${PROJECT_NAME} ${SRC_LIST}
#                    ${CPP_SOURCES}
#                    ${PRV_HEADERS}
#                    ${PUB_HEADERS}
    )

#add_executable(${PROJECT_NAME}
#  main.cpp
#)
#target_link_libraries(${PROJECT_NAME} Qt${QT_VERSION_MAJOR}::Core)

```