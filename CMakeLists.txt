project(qm2cm)
set(CMAKE_VERBOSE_MAKEFILE ON)
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)
cmake_minimum_required(VERSION 3.6)
#find_package(Qt5Core  REQUIRED)
find_package(Qt5 COMPONENTS Core Widgets REQUIRED)
#find_package(Qt5${_module_dep}
#        ${_Qt5Core_DEPENDENCIES_FIND_QUIET}
#        ${_Qt5Core_FIND_DEPENDENCIES_REQUIRED}
#        PATHS "${_qt5Core_install_prefix}" NO_DEFAULT_PATH
#        )

set(CMAKE_INCLUDE_CURRENT_DIR ON)
include_directories(

        ${Qt5Core_INCLUDE_DIRS}
        ${Qt5Gui_INCLUDE_DIRS}
        ${Qt5Widgets_INCLUDE_DIRS}
)

#
# Thanks, the first suggestion seems to work. Regarding the second I edited the question, I didn't include ${QT_USE_FILE},
# it was a copying error. Seems that include(${QT_USE_FILE}) is also not necessary. qt5_use_modules(${PROJECT_NAME} Widgets)
# should take care of it.
#        ${QT_USE_FILE}
#

include_directories(${QT_INCLUDES} ${CMAKE_CURRENT_BINARY_DIR})

set(qm2cm_SRCS converter.cpp qm2cm.cpp main.cpp)
set(qm2cm_UIS qm2cm.ui)

set(CMAKE_AUTOMOC ON)
qt5_wrap_ui(qm2cm_wrapped_UIS ${qm2cm_UIS})
#qt5_automoc(${qm2cm_SRCS})
qt_wrap_cpp(${qm2cm_SRCS})

add_executable(qm2cm ${qm2cm_SRCS} ${qm2cm_wrapped_UIS})
#target_link_libraries(qm2cm ${QT_QTCORE_LIBRARY} ${QT_QTGUI_LIBRARY})
target_link_libraries(qm2cm  ${Qt5Core_LIBRARIES} ${Qt5Widgets_LIBRARIES})
