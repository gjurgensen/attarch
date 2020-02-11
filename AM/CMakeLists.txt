cmake_minimum_required(VERSION 3.10.2)
project(CakemlAM C ASM)

include(CakeMLHelper.cmake)

set(am_src src/hello.sml src/world.sml)

cakeml_component(AM
    CML_SOURCES "${am_src}"
)
