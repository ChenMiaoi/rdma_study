cmake_minimum_required(VERSION 3.5.0)
project(rdma_study VERSION 0.1.0 LANGUAGES C CXX)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(PkgConfig REQUIRED)
pkg_check_modules(LIBIBVERBS REQUIRED libibverbs)
pkg_check_modules(LIBRDMACM REQUIRED librdmacm)

include_directories(
    ${LIBIBVERBS_INCLUDE_DIRS}
    ${LIBRDMACM_INCLUDE_DIRS}
)

link_directories(
    ${LIBIBVERBS_LIBRARY_DIRS}
    ${LIBRDMACM_LIBRARY_DIRS}
)

add_definitions(${LIBIBVERBS_CFLAGS_OTHER})
add_definitions(${LIBRDMACM_CFLAGS_OTHER})

add_executable(rdma_study main.cc)
target_link_libraries(rdma_study
    ${LIBIBVERBS_LIBRARIES}
    ${LIBRDMACM_LIBRARIES}
)

add_subdirectory(${CMAKE_SOURCE_DIR}/example)
