CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

PROJECT(APNGASM_TEST)

INCLUDE_DIRECTORIES(${PROJECT_BINARY_DIR}/src)

ENABLE_TESTING()
# Generate executable file
ADD_EXECUTABLE(apngasm-test
	EXCLUDE_FROM_ALL
    ${PROJECT_SOURCE_DIR}/apngtest.cpp
)

SET_TARGET_PROPERTIES(apngasm-test
	PROPERTIES OUTPUT_NAME apngtest)

LINK_DIRECTORIES(${PROJECT_BINARY_DIR}/../lib)
INCLUDE_DIRECTORIES(
  ${PROJECT_SOURCE_DIR}/../lib/src
  ${PROJECT_BINARY_DIR}/../lib/src
)
TARGET_LINK_LIBRARIES(apngasm-test apngasm)

ADD_TEST(
	NAME apngasm-test
	COMMAND apngasm-test
)

FIND_PACKAGE(ZLIB REQUIRED)
INCLUDE_DIRECTORIES(${ZLIB_INCLUDE_DIRS})
TARGET_LINK_LIBRARIES(apngasm-test ${ZLIB_LIBRARIES})

FILE(COPY ${PROJECT_SOURCE_DIR}/samples DESTINATION ./)
FILE(MAKE_DIRECTORY ${PROJECT_BINARY_DIR}/out)
