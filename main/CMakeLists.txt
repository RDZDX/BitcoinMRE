set(TARGET_NAME "main")

set(UBITCOIN_DIR ${CMAKE_SOURCE_DIR}/src/uBitcoin/src)
set(ZBAR_DIR ${CMAKE_SOURCE_DIR}/src/zbar)

set(LIB_SRCS
    ${UBITCOIN_DIR}/BaseClasses.cpp
    ${UBITCOIN_DIR}/Bitcoin.cpp
    ${UBITCOIN_DIR}/BitcoinCurve.cpp
    ${UBITCOIN_DIR}/Conversion.cpp
    ${UBITCOIN_DIR}/Electrum.cpp
    ${UBITCOIN_DIR}/HDWallet.cpp
    ${UBITCOIN_DIR}/Hash.cpp
    ${UBITCOIN_DIR}/PSBT.cpp
    ${UBITCOIN_DIR}/Script.cpp
    ${UBITCOIN_DIR}/Transaction.cpp
    ${UBITCOIN_DIR}/utility/segwit_addr.c
    ${UBITCOIN_DIR}/utility/trezor/address.c
    ${UBITCOIN_DIR}/utility/trezor/base58.c
    ${UBITCOIN_DIR}/utility/trezor/bignum.c
    ${UBITCOIN_DIR}/utility/trezor/bip39.c
    ${UBITCOIN_DIR}/utility/trezor/chacha_drbg.c
    ${UBITCOIN_DIR}/utility/trezor/chacha20poly1305/chacha_merged.c
    ${UBITCOIN_DIR}/utility/trezor/ecdsa.c
    ${UBITCOIN_DIR}/utility/trezor/hasher.c
    ${UBITCOIN_DIR}/utility/trezor/hmac.c
    ${UBITCOIN_DIR}/utility/trezor/memzero.c
    ${UBITCOIN_DIR}/utility/trezor/pbkdf2.c
    ${UBITCOIN_DIR}/utility/trezor/rand.c
    ${UBITCOIN_DIR}/utility/trezor/rfc6979.c
    ${UBITCOIN_DIR}/utility/trezor/ripemd160.c
    ${UBITCOIN_DIR}/utility/trezor/secp256k1.c
    ${UBITCOIN_DIR}/utility/trezor/sha2.c
    ${UBITCOIN_DIR}/utility/trezor/sha3.c
    ${CMAKE_SOURCE_DIR}/src/tiny-AES-c/aes.c
    ${CMAKE_SOURCE_DIR}/src/tiny-AES-c/pkcs7_padding.c
    ${CMAKE_SOURCE_DIR}/src/reedsolomon-c/reedsolomon.c
    ${CMAKE_SOURCE_DIR}/src/QRCode/qrcode_encoder.c
    ${ZBAR_DIR}/config.c
    ${ZBAR_DIR}/convert.c
    ${ZBAR_DIR}/decoder.c
    ${ZBAR_DIR}/error.c
    ${ZBAR_DIR}/image.c
    ${ZBAR_DIR}/img_scanner.c
    ${ZBAR_DIR}/processor.c
    ${ZBAR_DIR}/refcnt.c
    ${ZBAR_DIR}/scanner.c
    ${ZBAR_DIR}/svg.c
    ${ZBAR_DIR}/symbol.c
    ${ZBAR_DIR}/video.c
    ${ZBAR_DIR}/window.c
    ${ZBAR_DIR}/decoder/qr_finder.c
    ${ZBAR_DIR}/processor/lock.c
    ${ZBAR_DIR}/qrcode/bch15_5.c
    ${ZBAR_DIR}/qrcode/binarize.c
    ${ZBAR_DIR}/qrcode/isaac.c
    ${ZBAR_DIR}/qrcode/qrdec.c
    ${ZBAR_DIR}/qrcode/qrdectxt.c
    ${ZBAR_DIR}/qrcode/rs.c
    ${ZBAR_DIR}/qrcode/util.c
)

set(SOURCES
    BitcoinMRE.c
    bitcoin_mre.cpp
    nuklear_mre.c
    mre_io.c
    ${LIB_SRCS}
)

add_exec_vxp(${TARGET_NAME}
    SRCS ${SOURCES}
    RESOURCES resources
    APP_NAME "${APP_NAME}"
    APPID "${APPID}"
    BACKGROUND ${BACKGROUND}
    API "${API}"
    RAM "${RAM}"
)

target_include_directories(${TARGET_NAME} PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_SOURCE_DIR}/ResID
    ${CMAKE_SOURCE_DIR}/src/tiny-AES-c
    ${CMAKE_SOURCE_DIR}/src/reedsolomon-c
    ${CMAKE_SOURCE_DIR}/src/QRCode
    ${UBITCOIN_DIR}
    ${UBITCOIN_DIR}/utility
    ${UBITCOIN_DIR}/utility/trezor
    ${ZBAR_DIR}
    ${ZBAR_DIR}/qrcode
    ${ZBAR_DIR}/decoder
)

target_compile_options(${TARGET_NAME} PRIVATE
    $<$<COMPILE_LANGUAGE:CXX>:-fno-exceptions -fno-rtti>
    -w
)

target_link_libraries(${TARGET_NAME} mreapi)
