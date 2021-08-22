set(CAmkES true)

get_files(camkes_src
    ${cop_src} ${crypto_src} ../../am/CommTypes.sml 
    ../../system/camkes/dataports/DataportFFI.sml
)
get_files(camkes_c_src
    ../../system/crypto/crypto_ffi.c ../../system/camkes/dataports/dataport_ffi.c
)

get_files(platam_src ${camkes_src} PlatAM.sml)

# Needs the case-versioned cake compiler
build_cake(platam.cake SOURCES "${platam_src}" ENTRY_NAME run)
DeclareCAmkESComponent(
    Platam 
    SOURCES ${camkes_c_src}
    LIBS platam.cake camkescakeml
)

# Add hacl

set(hacl_release_dir "${CMAKE_CURRENT_SOURCE_DIR}/../../../hacl-star/dist")
set(hacl_path    "${hacl_release_dir}/gcc-compatible")
set(kremlin_path "${hacl_release_dir}/kremlin/include")
set(kremlib_path "${hacl_release_dir}/kremlin/kremlib/dist/minimal")
set(hacl_sources ${hacl_path}/Hacl_Hash.c ${hacl_path}/Hacl_Ed25519.c ${hacl_path}/Hacl_Curve25519_51.c ${hacl_path}/Hacl_Chacha20_Vec32.c ${hacl_path}/Hacl_Chacha20.c)
DeclareCAmkESComponent(
    Platam
    SOURCES ${hacl_sources}
    # INCLUDES ${CMAKE_CURRENT_SOURCE_DIR}/include ${hacl_path} ${kremlin_path} ${kremlib_path}
    INCLUDES /usr/lib/gcc-cross/aarch64-linux-gnu/8/include ${hacl_path} ${kremlin_path} ${kremlib_path}
    C_FLAGS -include ${CMAKE_CURRENT_SOURCE_DIR}/hacl_config.h
)
 
get_absolute_source_or_binary(out /usr/lib/gcc-cross/aarch64-linux-gnu/8/include)
message(WARNING "absolute: ${out}")