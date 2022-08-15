cmake_minimum_required(VERSION 3.9)
project (Benchmark)

add_executable(${PROJECT_NAME})
add_executable(IFE::${PROJECT_NAME} ALIAS ${PROJECT_NAME})

set_target_properties(${PROJECT_NAME} PROPERTIES
  CXX_STANDARD 17
  CXX_STANDARD_REQUIRED ON
  CXX_EXTENSIONS OFF
  OUTPUT_NAME ife-banchmark
  )

target_include_directories(${PROJECT_NAME}
  PRIVATE
  ${CMAKE_CURRENT_LIST_DIR}/include/
  $<TARGET_PROPERTY:IFE::IFE,INTERFACE_INCLUDE_DIRECTORIES>
  )

target_link_libraries(${PROJECT_NAME}
  PRIVATE
  IFE::IFE
  )

set(HEADERS
  include/BenchEventVsCall.h
  include/Test.h
  )
set(SOURCES
  src/main.cpp
  )
source_group(TREE ${CMAKE_CURRENT_LIST_DIR}/include/
  PREFIX ""
  FILES ${HEADERS}
  )
source_group(TREE ${CMAKE_CURRENT_LIST_DIR}/src/
  PREFIX ""
  FILES ${SOURCES}
  )
target_sources(${PROJECT_NAME}
  PRIVATE
  # ${HEADERS}
  ${SOURCES}
  )

if(NOT IFE_BUNDLED)
  install(TARGETS ${PROJECT_NAME}
    EXPORT ${IFE_TARGETS}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    )
endif()
