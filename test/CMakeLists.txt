
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/include ${PROJECT_SOURCE_DIR}/deps/geom/include
    ${PROJECT_SOURCE_DIR}/deps/cxxcam/include ${PROJECT_SOURCE_DIR}/src)

MACRO(CAMMACHINE_TEST testname)
	ADD_EXECUTABLE(${testname} EXCLUDE_FROM_ALL "${testname}.cpp")
	TARGET_LINK_LIBRARIES(${testname} cxxcam svg_path camMachine)
	SET_TARGET_PROPERTIES(${testname} PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR})
	ADD_TEST(${testname} "${MAKE_CURRENT_BINARY_DIR}/${testname}")
	ADD_DEPENDENCIES(check ${testname})
ENDMACRO()

FOREACH(test 
fold_adjacent
mill_basic 
lathe_basic 
model 
pushpop_state 
configuration 
inverse_time 
simulate_path 
simulate_path-test2 
simulate_path-nintynonmanifold 
# simulate_rotary 
simulate_arc 
simulate_arc_rotary 
sim_low_angular_res 
simulate_cut_air 
playjs 
play 
ex_newsim 
)
    CAMMACHINE_TEST(${test})
ENDFOREACH()

