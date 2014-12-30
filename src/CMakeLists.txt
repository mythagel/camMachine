FIND_PACKAGE(Boost 1.52.0 REQUIRED)
FIND_PACKAGE(Threads REQUIRED)

IF(UNIX)
	SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra")
ENDIF()

SET(CXXCAM_INCLUDE_DIR ${PROJECT_SOURCE_DIR}/deps/cxxcam/include)
SET(GEOM_INCLUDE_DIR ${PROJECT_SOURCE_DIR}/deps/geom/include)
INCLUDE_DIRECTORIES(${CAMMACHINE_INCLUDE_DIR} ${GEOM_INCLUDE_DIR} ${CXXCAM_INCLUDE_DIR} ${Boost_INCLUDE_DIRS})
ADD_LIBRARY(camMachine STATIC 
MachineState.cpp 
Machine.cpp 
Stock.cpp 
ToolTable.cpp 
Configuration.cpp 
Simulation.cpp 
GCodeBlock.cpp
GCode.cpp
Tool.cpp
)
TARGET_LINK_LIBRARIES(camMachine cxxcam geom ${CMAKE_THREAD_LIBS_INIT} ${Boost_LIBRARIES})
