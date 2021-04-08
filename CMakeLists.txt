cmake_minimum_required(VERSION 3.13)

project(docker-ecal)

option(DOCKER_ECAL_UPGRADE_OS_BASE     "Upgrade (pull) the OS base images"                            ON)
option(DOCKER_ECAL_USE_CACHE           "Use cache when building docker images"                        ON)
option(DOCKER_ECAL_BUILD_BIONIC        "Build with Ubuntu Bionic Beaver as a base"                    ON)
option(DOCKER_ECAL_BUILD_FOCAL         "Build with Ubuntu Focal Fossa as a base"                      ON)
option(DOCKER_ECAL_BUILD_ARCHLINUX     "Build with ArchLinux as a base"                              OFF)
option(DOCKER_ECAL_BUILD_ARCHLINUX_AUR "Build with Archlinux as a base for AUR package development"  OFF)
option(DOCKER_ECAL_BUILD_V5_7_9        "Build image for eCAL v5.7.9"                                  ON)
option(DOCKER_ECAL_BUILD_V5_8_5        "Build image for eCAL v5.8.5"                                  ON)

set(DOCKER_ECAL_TAG_PREFIX "blutkoete/")

add_custom_target(docker-ecal ALL)

if(${DOCKER_ECAL_UPGRADE_OS_BASE})
    set(DOCKER_ECAL_PULL "--pull")
endif()

if(NOT ${DOCKER_ECAL_USE_CACHE})
    set(DOCKER_ECAL_CACHE "--no-cache")
endif()

if(DOCKER_ECAL_BUILD_BIONIC)
    add_custom_target(ecal-base-bionic
                      docker build ${DOCKER_ECAL_CACHE} ${DOCKER_ECAL_PULL} --tag ${DOCKER_ECAL_TAG_PREFIX}ecal-base:latest-bionic-${CMAKE_SYSTEM_PROCESSOR} ${CMAKE_SOURCE_DIR}/ecal-base-bionic)
    add_dependencies(docker-ecal ecal-base-bionic)

    if(DOCKER_ECAL_BUILD_V5_7_9)
        add_custom_target(ecal-bionic-V5_7_9
                          docker build ${DOCKER_ECAL_CACHE} --tag ${DOCKER_ECAL_TAG_PREFIX}ecal:v5.7.9-bionic-${CMAKE_SYSTEM_PROCESSOR} --build-arg TAG=v5.7.9 --build-arg OS=bionic --build-arg ARCH=${CMAKE_SYSTEM_PROCESSOR} ${CMAKE_SOURCE_DIR}/ecal)
        add_dependencies(ecal-bionic-V5_7_9 ecal-base-bionic)
        add_dependencies(docker-ecal ecal-bionic-V5_7_9)
    endif()

    if(DOCKER_ECAL_BUILD_V5_8_5)
        add_custom_target(ecal-bionic-V5_8_5
                          docker build ${DOCKER_ECAL_CACHE} --tag ${DOCKER_ECAL_TAG_PREFIX}ecal:v5.8.5-bionic-${CMAKE_SYSTEM_PROCESSOR} --build-arg TAG=v5.8.5 --build-arg OS=bionic --build-arg ARCH=${CMAKE_SYSTEM_PROCESSOR} ${CMAKE_SOURCE_DIR}/ecal)
        add_dependencies(ecal-bionic-V5_8_5 ecal-base-bionic)
        add_dependencies(docker-ecal ecal-bionic-V5_8_5)
    endif()
endif()

if(DOCKER_ECAL_BUILD_FOCAL)
    add_custom_target(ecal-base-focal
                      docker build ${DOCKER_ECAL_CACHE} ${DOCKER_ECAL_PULL} --tag ${DOCKER_ECAL_TAG_PREFIX}ecal-base:latest-focal-${CMAKE_SYSTEM_PROCESSOR} ${CMAKE_SOURCE_DIR}/ecal-base-focal)
    add_dependencies(docker-ecal ecal-base-focal)

    if(DOCKER_ECAL_BUILD_V5_7_9)
        add_custom_target(ecal-focal-V5_7_9
                          docker build ${DOCKER_ECAL_CACHE} --tag ${DOCKER_ECAL_TAG_PREFIX}ecal:v5.7.9-focal-${CMAKE_SYSTEM_PROCESSOR} --build-arg TAG=v5.7.9 --build-arg OS=focal --build-arg ARCH=${CMAKE_SYSTEM_PROCESSOR} ${CMAKE_SOURCE_DIR}/ecal)
        add_dependencies(ecal-focal-V5_7_9 ecal-base-focal)
        add_dependencies(docker-ecal ecal-focal-V5_7_9)
    endif()

    if(DOCKER_ECAL_BUILD_V5_8_5)
        add_custom_target(ecal-focal-V5_8_5
                          docker build ${DOCKER_ECAL_CACHE} --tag ${DOCKER_ECAL_TAG_PREFIX}ecal:v5.8.5-focal-${CMAKE_SYSTEM_PROCESSOR} --build-arg TAG=v5.8.5 --build-arg OS=focal --build-arg ARCH=${CMAKE_SYSTEM_PROCESSOR} ${CMAKE_SOURCE_DIR}/ecal)
        add_dependencies(ecal-focal-V5_8_5 ecal-base-focal)
        add_dependencies(docker-ecal ecal-focal-V5_8_5)
    endif()
endif()

if(DOCKER_ECAL_BUILD_ARCHLINUX)
    add_custom_target(ecal-base-archlinux
                      docker build ${DOCKER_ECAL_CACHE} ${DOCKER_ECAL_PULL} --tag ${DOCKER_ECAL_TAG_PREFIX}ecal-base:latest-archlinux-${CMAKE_SYSTEM_PROCESSOR} ${CMAKE_SOURCE_DIR}/ecal-base-archlinux)
    add_dependencies(docker-ecal ecal-base-archlinux)

    if(DOCKER_ECAL_BUILD_V5_7_9)
        add_custom_target(ecal-archlinux-V5_7_9
                          docker build ${DOCKER_ECAL_CACHE} --tag ${DOCKER_ECAL_TAG_PREFIX}ecal:v5.7.9-archlinux-${CMAKE_SYSTEM_PROCESSOR} --build-arg TAG=v5.7.9 --build-arg OS=archlinux --build-arg ARCH=${CMAKE_SYSTEM_PROCESSOR} ${CMAKE_SOURCE_DIR}/ecal)
        add_dependencies(ecal-archlinux-V5_7_9 ecal-base-archlinux)
        add_dependencies(docker-ecal ecal-archlinux-V5_7_9)
    endif()

    if(DOCKER_ECAL_BUILD_V5_8_5)
        add_custom_target(ecal-archlinux-V5_8_5
                          docker build ${DOCKER_ECAL_CACHE} --tag ${DOCKER_ECAL_TAG_PREFIX}ecal:v5.8.5-archlinux-${CMAKE_SYSTEM_PROCESSOR} --build-arg TAG=v5.8.5 --build-arg OS=archlinux --build-arg ARCH=${CMAKE_SYSTEM_PROCESSOR} ${CMAKE_SOURCE_DIR}/ecal)
        add_dependencies(ecal-archlinux-V5_8_5 ecal-base-archlinux)
        add_dependencies(docker-ecal ecal-archlinux-V5_8_5)
    endif()
endif()

if(DOCKER_ECAL_BUILD_ARCHLINUX_AUR)
    add_custom_target(ecal-base-archlinux-aur
                      docker build ${DOCKER_ECAL_CACHE} ${DOCKER_ECAL_PULL} --tag ${DOCKER_ECAL_TAG_PREFIX}ecal-base:latest-archlinux-aur-${CMAKE_SYSTEM_PROCESSOR} ${CMAKE_SOURCE_DIR}/ecal-base-archlinux-aur)
    add_dependencies(docker-ecal ecal-base-archlinux-aur)
endif()
