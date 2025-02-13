project(assessment_tool)

set(CMAKE_AUTOMOC ON)

include_directories(${OMIM_ROOT}/3party/glm)

set(
  SRC
  assessment_tool.cpp
  context.cpp
  context.hpp
  edits.cpp
  edits.hpp
  feature_info_dialog.cpp
  feature_info_dialog.hpp
  helpers.cpp
  helpers.hpp
  main_model.cpp
  main_model.hpp
  main_view.cpp
  main_view.hpp
  model.hpp
  result_view.cpp
  result_view.hpp
  results_view.cpp
  results_view.hpp
  sample_view.cpp
  sample_view.hpp
  samples_view.cpp
  samples_view.hpp
  search_request_runner.cpp
  search_request_runner.hpp
  view.hpp
)

omim_add_executable(${PROJECT_NAME} MACOSX_BUNDLE ${SRC})
target_link_libraries(${PROJECT_NAME} gflags::gflags)

omim_link_libraries(
  ${PROJECT_NAME}
  qt_common
  map
  ge0
  drape_frontend
  shaders
  routing
  search_quality
  search_tests_support
  search
  storage
  tracking
  traffic
  routing_common
  transit
  descriptions
  drape
  kml
  editor
  indexer
  platform
  mwm_diff
  bsdiff
  geometry
  coding
  base
  expat
  freetype
  icu
  agg
  jansson
  minizip
  oauthcpp
  opening_hours
  openlr
  protobuf
  pugixml
  sdf_image
  stb_image
  succinct
  vulkan_wrapper
  ${Qt5Widgets_LIBRARIES}
  ${LIBZ}
)

if (PLATFORM_LINUX)
  omim_link_libraries(
    ${PROJECT_NAME}
    dl
  )
endif()

link_opengl(${PROJECT_NAME})
link_qt5_core(${PROJECT_NAME})
link_qt5_network(${PROJECT_NAME})

if (PLATFORM_MAC)
  set_target_properties(
    ${PROJECT_NAME}
    PROPERTIES
    MACOSX_BUNDLE_INFO_PLIST ${PROJECT_SOURCE_DIR}/Info.plist
  )
endif()
