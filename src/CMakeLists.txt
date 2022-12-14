add_executable(camera WIN32
    main.cpp
    camexamp.cpp
    viewer.cpp
)

target_link_libraries(camera
    PRIVATE
        librw::skeleton
        librw::librw
)

set_target_properties(
    camera PROPERTIES
    VS_DEBUGGER_WORKING_DIRECTORY "$<TARGET_FILE_DIR:camera>")

add_custom_command(
    TARGET camera POST_BUILD
    COMMAND "${CMAKE_COMMAND}" -E make_directory "$<TARGET_FILE_DIR:camera>/files"
    COMMAND "${CMAKE_COMMAND}" -E copy_directory "${CMAKE_CURRENT_SOURCE_DIR}/../data" "$<TARGET_FILE_DIR:camera>/files"
)
