set(HEADERS
  chat_api.h
  mt_net.h
  mtclient.h
  mtgametrack.h
  mtpilottrack.h
  mtstrings.h)
set(CPPS
  chat_api.cpp
  mt_net.cpp
  mtclient.cpp
  mtgametrack.cpp
  mtpilottracker.cpp
)

add_library(Parallax_Online MODULE ${HEADERS} ${CPPS})
set_target_properties(Parallax_Online PROPERTIES PREFIX "")
set_target_properties(Parallax_Online PROPERTIES CXX_VISIBILITY_PRESET "hidden")
set_target_properties(Parallax_Online PROPERTIES OUTPUT_NAME "Parallax Online")
target_link_libraries(Parallax_Online PRIVATE
  ddio
  inetfile
  misc
  ui
  $<$<PLATFORM_ID:Windows>:ws2_32>
)
if(CMAKE_SYSTEM_NAME STREQUAL "Darwin")
  set_target_properties(Parallax_Online PROPERTIES SUFFIX ".dylib")
endif()

add_custom_target(Parallax_Online_Hog
  COMMAND $<TARGET_FILE:HogMaker>
  "$<TARGET_FILE_DIR:Descent3>/online/Parallax Online.d3c"
  "${CMAKE_SOURCE_DIR}/netcon/mtclient/Parallax_Online.d3c.txt"
  "${CMAKE_SOURCE_DIR}/scripts/data/fullhog/"
  "$<TARGET_FILE_DIR:Parallax_Online>"

  DEPENDS Parallax_Online HogMaker
  COMMENT "Generate 'Parallax Online.d3c'"
)
install(FILES "$<TARGET_FILE_DIR:Descent3>/online/Parallax Online.d3c" DESTINATION ${CMAKE_INSTALL_DATADIR}/online)
