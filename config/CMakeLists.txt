cmake_minimum_required(VERSION 3.20.0)

# ビルド直前に問題のファイルを自動修正するスクリプト
set(TARGET_FILE "${WEST_TOPDIR}/zmk-module-runtime-input-processor/src/pointing/input_processor_runtime.c")

if(EXISTS ${TARGET_FILE})
    message(STATUS "[PATCH] Fixing input_processor_runtime.c argument compatibility...")
    file(READ ${TARGET_FILE} FILE_CONTENTS)
    string(REPLACE 
        "zmk_keymap_layer_activate(data->temp_layer_layer, false)" 
        "zmk_keymap_layer_activate(data->temp_layer_layer)" 
        MODIFIED_CONTENTS "${FILE_CONTENTS}")
    file(WRITE ${TARGET_FILE} "${MODIFIED_CONTENTS}")
endif()
