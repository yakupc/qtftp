#
# Copyright (C) 2024 Yakup Cengiz
#

# Set up the QtFtp library
file(GLOB QtFtp_SOURCES
    ${PROJECT_SOURCE_DIR}/src/qftp/*.?pp
)

file(GLOB QtFtp_HEADERS
    ${PROJECT_SOURCE_DIR}/src/qftp/*.h
)

add_library(QtFtp ${QtFtp_SOURCES} ${QtFtp_HEADERS})
add_library(Qt::Ftp ALIAS QtFtp)

# Additional setup
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

include_directories(${PROJECT_SOURCE_DIR}/src/qftp)

# Specify include directories
target_include_directories(QtFtp PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

# Link against Qt6 Core and Network modules
target_link_libraries(QtFtp PUBLIC Qt6::Core Qt6::Network)

# Set C++ standard
set_target_properties(QtFtp PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED ON
)

# Install targets
install(TARGETS QtFtp EXPORT QtFtpTargets
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
)

#set_target_properties(FieldLink PROPERTIES
#  RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
#  ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
#  LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
#)

install(FILES ${QtFtp_HEADERS}
    DESTINATION include/QtFtp
)
