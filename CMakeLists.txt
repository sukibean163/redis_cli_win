cmake_minimum_required(VERSION 2.8)
project(redis_cli_win)




file(GLOB_RECURSE SOURCE_FILES src/*.cpp)
file(GLOB_RECURSE HEADER_FILES include/*.h)

include_directories(
    include    
    hiredis/include    
)



add_executable(${PROJECT_NAME}
  ${SOURCE_FILES}
  ${HEADER_FILES}
)


# link_directories(${CMAKE_CURRENT_LIST_DIR}/../${PROJECT_NAME}/hiredis/lib)
target_link_libraries(${PROJECT_NAME}
    ${CMAKE_CURRENT_LIST_DIR}/hiredis/lib/hiredis.lib
    ws2_32.lib
)

# add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
#                    COMMAND cp ${CMAKE_CURRENT_SOURCE_DIR}/hiredis/lib/hiredis.dll ${CMAKE_CURRENT_BINARY_DIR})
install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/hiredis/lib/hiredis.dll DESTINATION ${${CMAKE_INSTALL_PREFIX}}/lib )
# install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/hiredis/lib/hiredis.dll DESTINATION ${${CMAKE_CURRENT_BINARY_DIR}})
install(TARGETS ${PROJECT_NAME} 
        DESTINATION lib
        )
install(DIRECTORY include/
        DESTINATION include)