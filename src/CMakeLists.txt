######################################################################################
# Build function for main library
######################################################################################

IF(NOT WIN32)
  INCLUDE_DIRECTORIES(.)
  SET(SRCS lightstone.c lightstone_libusb1.c)

  BUILDSYS_BUILD_LIB(
    NAME lightstone
    SOURCES "${SRCS}" 
    CXX_FLAGS FALSE
    LINK_LIBS ${LIBLIGHTSTONE_DEP_LIBS}
    LINK_FLAGS FALSE
    DEPENDS FALSE
    SHOULD_INSTALL TRUE
    VERSION "${LIBLIGHTSTONE_VERSION}"
    )
ELSE()
  INCLUDE_DIRECTORIES(../libnputil/include/ .)
  SET(SRCS lightstone.c lightstone_win32.c)

  #SET(DEFS "-DUSE_WIN32")

  IF(BUILD_SHARED)
    LIST(APPEND DEFS "-DLIGHTSTONE_DYNAMIC")
  ENDIF()

  BUILDSYS_BUILD_LIB(
    NAME lightstone
    SOURCES "${SRCS}" 
    CXX_FLAGS "${DEFS}"
    LINK_LIBS ${LIBLIGHTSTONE_DEP_LIBS}
    LINK_FLAGS FALSE
    DEPENDS FALSE
    SHOULD_INSTALL TRUE
    VERSION "${LIBLIGHTSTONE_VERSION}"
    )
ENDIF()
