cmake_minimum_required(VERSION 3.16)

project(dir-utilities VERSION 0.1 LANGUAGES CXX)

set(CMAKE_AUTOMOC ON)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 6.2 COMPONENTS Quick REQUIRED)

qt_add_executable(appdir-utilities
    searchmodel.h
    searchmodel.cpp
    main.cpp
)

qt_add_qml_module(appdir-utilities
    URI dir-utilities
    VERSION 1.0
    QML_FILES main.qml UtilFiles.qml
)

set_target_properties(appdir-utilities PROPERTIES
    MACOSX_BUNDLE_GUI_IDENTIFIER my.example.com
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

target_compile_definitions(appdir-utilities
    PRIVATE $<$<OR:$<CONFIG:Debug>,$<CONFIG:RelWithDebInfo>>:QT_QML_DEBUG>)
target_link_libraries(appdir-utilities
    PRIVATE Qt6::Quick)