SET(SRC 
defines.h
utilSocket.c
utilSocket.h
utilXml.c
utilXml.h
) 

IF( WIN32 )
  LIST( APPEND SRC bcvtb.def )
ENDIF()

INCLUDE_DIRECTORIES( "${CMAKE_SOURCE_DIR}/SourceCode/Expat/lib")

ADD_LIBRARY( bcvtb SHARED ${SRC} )

TARGET_LINK_LIBRARIES( bcvtb epexpat )

IF( WIN32 )
  TARGET_LINK_LIBRARIES( bcvtb wsock32 )
ENDIF()

set_target_properties(
  bcvtb
  PROPERTIES
  INSTALL_NAME_DIR "@executable_path/../lib"
)

INSTALL( TARGETS bcvtb 
  RUNTIME DESTINATION bin 
  LIBRARY DESTINATION lib 
)

