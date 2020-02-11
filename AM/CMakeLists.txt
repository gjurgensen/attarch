cmake_minimum_required(VERSION 3.10.2)
project(CakemlAM C ASM)

include(CakeMLHelper.cmake)

cakeml_component(AM
    CML_SOURCES "hello.sml;world.sml"
)
