# The following lines of boilerplate have to be in your project's
# CMakeLists in this exact order for cmake to work correctly
cmake_minimum_required(VERSION 3.16)

set(EXTRA_COMPONENT_DIRS
    ../../libs/adv_button
    ../../libs/adv_hlw
    ../../libs/adv_i2c
    ../../libs/adv_logger_ntp
    ../../libs/adv_pwm
    ../../libs/form_urlencoded
    ../../libs/new_dht
    ../../libs/new_onewire
    ../../libs/new_ds18b20
    ../../libs/timers_helper
    ../../libs/esp32_port
    ../../libs/unistring
    ../../libs/raven_ntp
    ../../libs/rs_ping
    ../../libs/cJSON-rsf
    ../../external_libs/wolfssl
    ../../libs/homekit-rsf
)

list(APPEND WOLFSSL_COMPILE_OPTIONS
    -DWOLFSSL_USER_SETTINGS
    -DWOLFSSL_STATIC_RSA
    -DWOLFSSL_SHA384
    -DWOLFSSL_SHA512
    -DUSE_SLOW_SHA
    -DUSE_SLOW_SHA2
    -DUSE_SLOW_SHA256
    -DUSE_SLOW_SHA512
    -DGCM_SMALL
    -DRSA_LOW_MEM
    -DHAVE_AESGCM
    -DHAVE_ECC
    -DHAVE_TLS_EXTENSIONS
    -DHAVE_ECC_DHE
    -DHAVE_SUPPORTED_CURVES
    -DHAVE_SNI
    -DNO_MD5
    -DNO_FILESYSTEM
    -DNO_WRITEV
    -DNO_WOLFSSL_SERVER
    -DNO_RABBIT
    -DNO_DH
    -DNO_PWDBASED
    -DNO_DES3
    -DNO_ERROR_STRINGS
    -DNO_OLD_TLS
    -DNO_RC4
    -DNO_PSK
    -DNO_MD4
    -DNO_HC128
    -DNO_DEV_RANDOM
    -DNO_SESSION_CACHE
    -DNO_DSA
    -DWOLFCRYPT_HAVE_SRP
    -DWOLFSSL_BASE64_ENCODE
    -DNO_SHA
    -DHAVE_HKDF
    -DHAVE_CHACHA
    -DHAVE_POLY1305
    -DHAVE_ED25519
    -DHAVE_CURVE25519
    -DHAVE_ONE_TIME_AUTH
    -DTFM_TIMING_RESISTANT
)

list(APPEND EXTRA_COMPILE_OPTIONS
    -DHOMEKIT_SHORT_APPLE_UUIDS
    -DHOMEKIT_DISABLE_MAXLEN_CHECK
    -DHOMEKIT_DISABLE_VALUE_RANGES
    -DHAA_CHIP_NAME="${IDF_TARGET}"
)

if(HAA_SINGLE_CORE)
    list(APPEND EXTRA_COMPILE_OPTIONS
        -DHAA_SINGLE_CORE
    )
endif()

if(HAA_XTAL26)
    list(APPEND EXTRA_COMPILE_OPTIONS
        -DHAA_XTAL26
    )
endif()

include($ENV{IDF_PATH}/tools/cmake/project.cmake)
project(HAA_Main)

idf_build_set_property(COMPILE_OPTIONS "${WOLFSSL_COMPILE_OPTIONS}" APPEND)
idf_build_set_property(COMPILE_OPTIONS "${EXTRA_COMPILE_OPTIONS}" APPEND)
