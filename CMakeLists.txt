# Set minimum CMake version
cmake_minimum_required(VERSION 3.16)

# Optional verbose mode, uncomment or pass in -DCMAKE_VERBOSE_MAKEFILE=ON
set(CMAKE_VERBOSE_MAKEFILE ON)

set(BASE_LOCATION .)

# Set the toolchain path
if (WIN32 OR MINGW)
    set(PLATFORM_WINDOWS 1)
    set(COMPILER_PREFIX "C:/Keil_v5/C51/BIN/")
elseif (UNIX)
    set(PLATFORM_UNIX 1)
    set(COMPILER_PREFIX "/replace/")
else ()
    message(FATAL_ERROR "Unsupported platform")
endif ()

# Set the compiler (must be prior to project setup)
include(${BASE_LOCATION}/cmake/arm-gcc.cmake)

##### Project Setup #####
# Configure project and languages
project(efm8-template C CXX ASM)

# Set build
if (NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug)
endif ()

if (CMAKE_BUILD_TYPE MATCHES Debug)
    message("Build type: Debug")

    # Set preprocessor definitions
    add_compile_definitions(
            DEBUG
    )
else ()
    message("Build type: Release")

    # Set preprocessor definitions
    add_compile_definitions(
            RELEASE
    )
endif ()

# ${DEVICE} sets the target specific model name
if (NOT DEVICE)
    set(DEVICE EFM8LB11F32E)  # Sets device / used to locate HAL files
endif ()

# Set linker script
set(LINKER_SCRIPT ${CMAKE_CURRENT_LIST_DIR}/cmake/linkerscript.ld)

##### Modules #####

# Libraries can be added to the LIBS variable
# or manually included here.

set(CMAKE_EXE_LINKER_FLAGS "${COMMON_DEFINITIONS} --specs=nosys.specs -Xlinker -T${LINKER_SCRIPT} -Wl,-Map=${CMAKE_CURRENT_BINARY_DIR}/${CMAKE_PROJECT_NAME}.map -Wl,--gc-sections -Wl,-v")

##### Files #####

# Add project headers
include_directories(
        C:/Keil_v5/C51/INC/
)

# Generate executable and link
add_executable(${PROJECT_NAME}
        source/HELLO.C
)

target_link_libraries(${PROJECT_NAME} ${LIBS} emlib cmsis)

##### Post build #####

# Add post build commands
include(${BASE_LOCATION}/cmake/post-build.cmake)

# Add JLink commands
include(${BASE_LOCATION}/cmake/jlink.cmake)
