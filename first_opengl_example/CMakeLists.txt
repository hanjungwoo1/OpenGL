cmake_minimum_required(VERSION 3.14)

set(PROJECT_NAME first_opengl_example)
set(CMAKE_CXX_STANDARD 17)

# GLFW로 윈도우를 생성하기
set(WINDOW_NAME "First OpenGL Example!")
set(WINDOW_WIDTH 960)
set(WINDOW_HEIGHT 540)

project(${PROJECT_NAME})
add_executable(${PROJECT_NAME} src/main.cpp)

include(Dependency.cmake)

# 우리 프로젝트에 include / lib 관련 옵션 추가
target_include_directories(${PROJECT_NAME} PUBLIC ${DEP_INCLUDE_DIR})
target_link_directories(${PROJECT_NAME} PUBLIC ${DEP_LIB_DIR})
target_link_libraries(${PROJECT_NAME} PUBLIC ${DEP_LIBS})

# GLFW로 윈도우를 생성하기
target_compile_definitions(${PROJECT_NAME} PUBLIC
    WINDOW_NAME="${WINDOW_NAME}"
    WINDOW_WIDTH=${WINDOW_WIDTH}
    WINDOW_HEIGHT=${WINDOW_HEIGHT}
    )


# Dependency들이 먼저 build 될 수 있게 관계 설정 -> 순서대로 하게
add_dependencies(${PROJECT_NAME} ${DEP_LIST})