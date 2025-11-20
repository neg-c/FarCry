project(FarCry)

set(SRC_FILES
    "FarCry.rc"
    "Main.cpp"
)

add_executable(${PROJECT_NAME} WIN32 ${SRC_FILES})

target_include_directories(${PROJECT_NAME} PRIVATE
    ${CMAKE_SOURCE_DIR}/Externals/SDL/include
)

target_link_libraries(${PROJECT_NAME} PRIVATE CryCommon SDL2 CrySystem)

# Ensure all game modules are built (even though they're loaded dynamically at runtime)
# This creates a build-order dependency without linking
add_dependencies(${PROJECT_NAME}
    CryGame
    Cry3DEngine
    CryAISystem
    CryAnimation
    CryEntitySystem
    CryFont
    CryNetwork
    CryPhysics
    CryScriptSystem
    CrySoundSystem
)

if (MSVC)
    add_dependencies(${PROJECT_NAME}
        CryInput
        CryMovie
        XRenderD3D9
    )
endif()

add_dependencies(${PROJECT_NAME}
    XRenderNULL
    XRenderOGL
)

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