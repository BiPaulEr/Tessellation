cmake_minimum_required(VERSION 3.0)

project(BaseGL)

add_subdirectory(External)

add_executable (
	BaseGL
	main.cpp
)

# Copy the shader files in the binary location. 
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_custom_command(TARGET BaseGL 
                   POST_BUILD
                   COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:BaseGL> ${CMAKE_CURRENT_SOURCE_DIR})

target_link_libraries(BaseGL LINK_PRIVATE glad)

target_link_libraries(BaseGL LINK_PRIVATE glfw)

target_link_libraries(BaseGL LINK_PRIVATE glm)

# Glew
target_include_directories(BaseGL PRIVATE ${PROJECT_SOURCE_DIR}/External/glew/include)
target_link_libraries(BaseGL LINK_PRIVATE ${PROJECT_SOURCE_DIR}/External/glew/lib/Release/x64/glew32s.lib) 
target_link_libraries(BaseGL LINK_PRIVATE ${PROJECT_SOURCE_DIR}/External/glew/lib/Release/x64/glew32.lib) 

#Glut
target_include_directories(BaseGL PRIVATE ${PROJECT_SOURCE_DIR}/External/glut/include)
target_link_libraries(BaseGL LINK_PRIVATE ${PROJECT_SOURCE_DIR}/External/glut/lib/x64/freeglut.lib) 