set(HEADERS
  debug.h
  debugbreak.h
  mono.h)
set(CPPS
  $<$<PLATFORM_ID:Darwin,Linux,OpenBSD>:
    lnxdebug.cpp
    lnxmono.cpp
  >
  $<$<PLATFORM_ID:Windows>:
    windebug.cpp
    winmono.cpp
  >
)

add_library(ddebug STATIC ${HEADERS} ${CPPS})
add_dependencies(ddebug get_git_hash)
target_include_directories(ddebug PUBLIC
  $<BUILD_INTERFACE:
  ${PROJECT_SOURCE_DIR}/ddebug
  >
  PRIVATE ${PROJECT_BINARY_DIR}/lib   # For d3_version.h
)
target_link_libraries(ddebug PRIVATE
  mem
  $<$<PLATFORM_ID:Windows>:
    misc
  >
)
