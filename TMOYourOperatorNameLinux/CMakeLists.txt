CMAKE_MINIMUM_REQUIRED(VERSION 2.4.8)
SET(CMAKE_COLOR_MAKEFILE ON)
SET(CMAKE_VERBOSE_MAKEFILE ON)
SET(CMAKE_INCLUDE_CURRENT_DIR TRUE)

IF(UNIX AND NOT LINUX_SET)
 ADD_DEFINITIONS(-D LINUX)
ENDIF(UNIX AND NOT LINUX_SET)

INCLUDE_DIRECTORIES(
../tmolib/
.
)

LINK_LIBRARIES (
tmo
)

SET(TMO_SOURCES
 TMOYourOperatorName.cpp
 TMOPlugin.cpp
)


SET(TMOWARD_HEADERS
 TMOYourOperatorName.h
 TMOPlugin.h
)


add_library( yourOperator SHARED ${TMO_SOURCES} )
add_custom_command( TARGET yourOperator POST_BUILD 
	COMMAND cp -f libyourOperator.so ../TMOCmd/yourOperator.tml
	COMMAND cp -f libyourOperator.so ../TMOgui/yourOperator.tml 
	COMMAND cp -f libyourOperator.so ../yourOperator.tml 
#	COMMAND rm -f libyourOperator.so 
	)


