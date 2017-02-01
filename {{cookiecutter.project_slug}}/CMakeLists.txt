cmake_minimum_required(VERSION {{ cookiecutter.minimum_cmake_version }})

include("cmake/HunterGate.cmake")

HunterGate(
    URL "https://github.com/ruslo/hunter/archive/{{ cookiecutter.hunter_gate_version }}.tar.gz"
    SHA1 "{{cookiecutter.hunter_gate_sha1}}"
    LOCAL
)

project({{ cookiecutter.project_slug }})
set(CMAKE_CXX_STANDARD {{ cookiecutter.cxx_standard }})

set(APPLICATION_NAME "{{ cookiecutter.project_slug }}")
set(APPLICATION_CODENAME "${PROJECT_NAME}")

set(APPLICATION_COPYRIGHT_YEARS "{{ cookiecutter.year }}")

# Application versioning.
set (APPLICATION_VERSION_MAJOR 0)
set (APPLICATION_VERSION_MINOR 1)
set (APPLICATION_VERSION_PATCH 0)
set (APPLICATION_VERSION_TYPE SNAPSHOT)
set (APPLICATION_VERSION_STRING "${APPLICATION_VERSION_MAJOR}.${APPLICATION_VERSION_MINOR}.${APPLICATION_VERSION_PATCH}-${APPLICATION_VERSION_TYPE}")

# Release config.
set (CMAKE_VERBOSE_MAKEFILE 0) # Use 1 for debugging, 0 for release.

# Set source/target.
set(SOURCE_FILES src/{{ cookiecutter.project_slug }}.cpp)
set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")

# Hunter packages. Don't forget to freeze versions via cmake/Hunter/config.cmake.
# hunter_add_package(spdlog)
# find_package(spdlog CONFIG REQUIRED)

include_directories(lib)
include_directories(include)

add_executable({{ cookiecutter.project_slug }} ${SOURCE_FILES})

target_link_libraries(
    {{ cookiecutter.project_slug }}
#    spdlog::spdlog
)
