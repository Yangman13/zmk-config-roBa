cmake_minimum_required(VERSION 3.20.0)

# ランダムな一時フォルダに対応するため、WEST_TOPDIRからの絶対パスを再定義
set(PATCH_TARGET "${WEST_TOPDIR}/zmk-module-runtime-input-processor/src/pointing/input_processor_runtime.c")

if(EXISTS "${PATCH_TARGET}")
    message(STATUS "[PATCH] Found input_processor_runtime.c, applying function argument fix...")
    file(READ "${PATCH_TARGET}" FILE_CONTENTS)
    
    # 引数が2つある古い記述を、1つの新しい記述に置換
    string(REPLACE 
        "zmk_keymap_layer_activate(data->temp_layer_layer, false)" 
        "zmk_keymap_layer_activate(data->temp_layer_layer)" 
        MODIFIED_CONTENTS "${FILE_CONTENTS}")
        
    file(WRITE "${PATCH_TARGET}" "${MODIFIED_CONTENTS}")
    message(STATUS "[PATCH] Successfully applied fix to input_processor_runtime.c!")
else()
    message(WARNING "[PATCH] Could not find target file at: ${PATCH_TARGET}")
endif()
