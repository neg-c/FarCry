project(FarCry)

set(SRC_FILES
    "FarCry.rc"
    "Main.cpp"
)

add_executable(${PROJECT_NAME} WIN32 ${SRC_FILES})

target_include_directories(${PROJECT_NAME} PRIVATE
    ${CMAKE_SOURCE_DIR}/SourceCode/CryCommon
    ${CMAKE_SOURCE_DIR}/Externals/SDL/include
)

target_link_libraries(${PROJECT_NAME} SDL2 CrySystem)

if (CMAKE_SIZEOF_VOID_P EQUAL 8)
    set(BIN_DIR "BinWin64")
else()
    set(BIN_DIR "BinWin32")
endif()

add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
    ${CMAKE_SOURCE_DIR}/${BIN_DIR}
    $<TARGET_FILE_DIR:${PROJECT_NAME}>
    COMMENT "Copying runtime dependencies from ${BIN_DIR} to output directory"
)