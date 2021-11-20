# CMake

### CONTENT
* CMake [Reminder][remind]

[reminder]: https://github.com/yoricsv/001_JMaven_/blob/master/res/read/Maven_Configuration.md


/**
  ******************************************************************************
  * @file           : README.md
  * @brief          : Short description of the project
  ******************************************************************************
  * @attention
  *
  * The PROJECT STRUCTURE part describes the common structure of the project
  * in order to understand where the code is and where the Cmake generator 
  * finds the source files.
  *
  ******************************************************************************
*/

## PROJECT STRUCTURE (blank)
```
[<Project_name>]
  |
  |->[.build]           // directory for building system
  |   |
  |   |->[CMakeFiles]   // all necessary directories and files for CMake build 
  |                     // generator
  |
  |->[.git]             // all necessary directories and files for Git
  |
  |
  |->[.settings]        // contains project file directories for different IDEs
  |
  |
  |->[debug]            // contains compiller, linker, object files
  |   |
  |   |->[logs]         // contains logs
  |
  |->[<Project_name Repository>]
  |   |
  |   |->[inc]          // contains public/private HEADERS (*.h) (might be split
  |   |                 // into two directories public and privat)
  |   |->[res]          // contains static/dynamic LIBRARIES     (might be split
  |   |                 // into two directories static and dynamic)
  |   |->[src]          // contains SOURCE files/code(s)   (.с; .cpp)
  |   |
  |   |->[ui]           // these directories for applications with USER INTERFACE
  |                     // (might contains QML)
  |
  |->[output]           // directory for executable applications
  |
  |->[tests]            // directory for unit tests
  |
  |
  |---> .gitignore
  |---> CMakeLists.txt
  |---> README.md
  ```