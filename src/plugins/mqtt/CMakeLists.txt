CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
PROJECT(TDengine)

IF ((TD_LINUX_64) OR (TD_LINUX_32 AND TD_ARM))
  INCLUDE_DIRECTORIES(${TD_COMMUNITY_DIR}/src/inc)
  INCLUDE_DIRECTORIES(${TD_COMMUNITY_DIR}/src/os/inc)
  INCLUDE_DIRECTORIES(${TD_COMMUNITY_DIR}/src/client/inc)
  INCLUDE_DIRECTORIES(${TD_COMMUNITY_DIR}/src/util/inc)
  INCLUDE_DIRECTORIES(${TD_COMMUNITY_DIR}/src/query/inc)
  INCLUDE_DIRECTORIES(${TD_COMMUNITY_DIR}/src/common/inc)
  INCLUDE_DIRECTORIES(${TD_COMMUNITY_DIR}/deps/cJson/inc)
  INCLUDE_DIRECTORIES(${TD_COMMUNITY_DIR}/deps/MQTT-C/include)
  INCLUDE_DIRECTORIES(${TD_COMMUNITY_DIR}/deps/MQTT-C/examples/templates)
  INCLUDE_DIRECTORIES(inc)
  AUX_SOURCE_DIRECTORY(src SRC)
  ADD_LIBRARY(mqtt ${SRC})
  TARGET_LINK_LIBRARIES(mqtt taos_static cJson mqttc)

  IF (TD_ADMIN)
    TARGET_LINK_LIBRARIES(mqtt admin cJson)
  ENDIF ()
ENDIF ()
