set(HEADERS monsterball.h monsterstr.h)
set(CPPS monsterball.cpp)

set(NETGAME_MODULE monsterball)

add_library(${NETGAME_MODULE} MODULE ${CPPS} ${HEADERS})
set_target_properties(${NETGAME_MODULE} PROPERTIES PREFIX "")
set_target_properties(${NETGAME_MODULE} PROPERTIES SUFFIX ".d3m")

target_link_libraries(${NETGAME_MODULE} dmfc)
