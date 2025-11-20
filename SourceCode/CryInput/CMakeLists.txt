project(CryInput)

add_definitions(-D_USRDLL -DCRYINPUT_EXPORTS)

set(SRC_FILES
    "CryInput.cpp"
    "Input.cpp"
    "Joystick.cpp"
    "StdAfx.cpp"
    "XActionMap.cpp"
    "XActionMapManager.cpp"
    "XKeyboard.cpp"
    "XMouse.cpp"
)

add_library(${PROJECT_NAME} SHARED ${SRC_FILES})

target_link_libraries(${PROJECT_NAME} PRIVATE CryCommon SDL2)
