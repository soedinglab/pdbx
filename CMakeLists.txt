cmake_minimum_required(VERSION 2.8.12)
project(pdbx)

set(PACKAGE_VERSION 1.0)

find_program(PYTHON "python3")

if(NOT DEFINED UserInstallOption)
    option(UserInstallOption "UserInstallOption" OFF)
endif()

if (PYTHON)
    set(SETUP_PY_IN "${CMAKE_CURRENT_SOURCE_DIR}/setup.py.in")
    set(SETUP_PY    "${CMAKE_CURRENT_BINARY_DIR}/setup.py")
    set(DEPS        "${CMAKE_CURRENT_SOURCE_DIR}/pdbx/__init__.py")
    set(OUTPUT      "${CMAKE_CURRENT_BINARY_DIR}/build/timestamp")

    configure_file(${SETUP_PY_IN} ${SETUP_PY})

    add_custom_command(OUTPUT ${OUTPUT}
        COMMAND ${PYTHON} ${SETUP_PY} build
        COMMAND ${CMAKE_COMMAND} -E touch ${OUTPUT}
        DEPENDS ${DEPS})

    add_custom_target(target ALL DEPENDS ${OUTPUT})

    if (UserInstallOption STREQUAL "ON")
        install(CODE "execute_process(COMMAND ${PYTHON} ${SETUP_PY} install --user)")
    else()
        install(CODE "execute_process(COMMAND ${PYTHON} ${SETUP_PY} install)")
    endif()
endif()
