cmake_minimum_required(VERSION 3.9)
project(IFE
  VERSION ${IFE_VERSION}
  LANGUAGES CXX
  )

add_library(${PROJECT_NAME} INTERFACE)
add_library(IFE::${PROJECT_NAME} ALIAS ${PROJECT_NAME})

#set_target_properties(${PROJECT_NAME}
#                      PROPERTIES
#                     )

target_include_directories(${PROJECT_NAME}
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/include/>
  $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDE_DIR}/>
  )

set(HEADERS
  include/ife/event.hpp
  include/ife/event_vector.hpp
  )
source_group(TREE ${CMAKE_CURRENT_LIST_DIR}/include/
  PREFIX ""
  FILES ${HEADERS}
  )
# target_sources(${PROJECT_NAME}
#   ${HEADERS}
#   )

if(NOT IFE_BUNDLED)
  install(TARGETS ${PROJECT_NAME}
    EXPORT ${IFE_TARGETS}
    INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/
    )
  install(DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/include/
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
    )
endif()
