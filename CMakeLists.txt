cmake_minimum_required(VERSION 3.15)
project(ble_app_template_pca10056_s140 C ASM)

if(NOT TOOLCHAIN_PATH)
     set(TOOLCHAIN_PATH "/usr")
     message(STATUS "No TOOLCHAIN_PATH specified, using default: " ${TOOLCHAIN_PATH})
else()
     file(TO_CMAKE_PATH "${TOOLCHAIN_PATH}" TOOLCHAIN_PATH)
endif()

if(NOT TOOLCHAIN_TRIPLET)
    set(TOOLCHAIN_TRIPLET "arm-none-eabi")
    message(STATUS "No TOOLCHAIN_TRIPLET specified, using default: " ${TOOLCHAIN_TRIPLET})
endif()

if(NOT NRF5_SDK_PATH)
     set(NRF5_SDK_PATH "/opt/nrf5-sdk")
     message(STATUS "No NRF5_SDK_PATH specified, using default: " ${NRF5_SDK_PATH})
else()
     file(TO_CMAKE_PATH "${NRF5_SDK_PATH}" NRF5_SDK_PATH)
endif()

set(TOOLCHAIN_BIN_PATH "${TOOLCHAIN_PATH}/bin")
set(TOOLCHAIN_INC_PATH "${TOOLCHAIN_PATH}/${TOOLCHAIN_TRIPLET}/include")
set(TOOLCHAIN_LIB_PATH "${TOOLCHAIN_PATH}/${TOOLCHAIN_TRIPLET}/lib")

set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)
set(CMAKE_C_COMPILER "${TOOLCHAIN_BIN_PATH}/${TOOLCHAIN_TRIPLET}-gcc")
set(CMAKE_CXX_COMPILER "${TOOLCHAIN_BIN_PATH}/${TOOLCHAIN_TRIPLET}-g++")
set(CMAKE_ASM_COMPILER "${TOOLCHAIN_BIN_PATH}/${TOOLCHAIN_TRIPLET}-gcc")
set(CMAKE_SIZE_BIN "${TOOLCHAIN_BIN_PATH}/${TOOLCHAIN_TRIPLET}-size")
set(CMAKE_OBJCOPY_BIN "${TOOLCHAIN_BIN_PATH}/${TOOLCHAIN_TRIPLET}-objcopy")

set(CMAKE_SYSTEM_NAME Generic)
set(CMAKE_SYSTEM_PROCESSOR arm)

# TARGETS?
set(LINKER_SCRIPT "ble_app_template_gcc_nrf52.ld")

# Setup output directories.
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}/bin")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}/lib")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}/lib")

add_executable(nrf52840_xxaa "main.c")

target_include_directories(nrf52840_xxaa
  PRIVATE
    "config/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/generic/message/"
    "${NRF5_SDK_PATH}/components/nfc/t2t_lib/"
    "${NRF5_SDK_PATH}/components/nfc/t4t_parser/hl_detection_procedure/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_ancs_c/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_ias_c/"
    "${NRF5_SDK_PATH}/components/libraries/pwm/"
    "${NRF5_SDK_PATH}/components/libraries/usbd/class/cdc/acm/"
    "${NRF5_SDK_PATH}/components/libraries/usbd/class/hid/generic/"
    "${NRF5_SDK_PATH}/components/libraries/usbd/class/msc/"
    "${NRF5_SDK_PATH}/components/libraries/usbd/class/hid/"
    "${NRF5_SDK_PATH}/modules/nrfx/hal/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/conn_hand_parser/le_oob_rec_parser/"
    "${NRF5_SDK_PATH}/components/libraries/log/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_gls/"
    "${NRF5_SDK_PATH}/components/libraries/fstorage/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/text/"
    "${NRF5_SDK_PATH}/components/libraries/mutex/"
    "${NRF5_SDK_PATH}/components/libraries/gpiote/"
    "${NRF5_SDK_PATH}/components/libraries/bootloader/ble_dfu/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/connection_handover/common/"
    "${NRF5_SDK_PATH}/components/boards/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/generic/record/"
    "${NRF5_SDK_PATH}/components/nfc/t4t_parser/cc_file/"
    "${NRF5_SDK_PATH}/components/ble/ble_advertising/"
    "${NRF5_SDK_PATH}/external/utf_converter/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_bas_c/"
    "${NRF5_SDK_PATH}/modules/nrfx/drivers/include/"
    "${NRF5_SDK_PATH}/components/libraries/experimental_task_manager/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_hrs_c/"
    "${NRF5_SDK_PATH}/components/softdevice/s140/headers/nrf52/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/connection_handover/le_oob_rec/"
    "${NRF5_SDK_PATH}/components/libraries/queue/"
    "${NRF5_SDK_PATH}/components/libraries/pwr_mgmt/"
    "${NRF5_SDK_PATH}/components/ble/ble_dtm/"
    "${NRF5_SDK_PATH}/components/toolchain/cmsis/include/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_rscs_c/"
    "${NRF5_SDK_PATH}/components/ble/common/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_lls/"
    "${NRF5_SDK_PATH}/components/libraries/bsp/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/connection_handover/ac_rec/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_bas/"
    "${NRF5_SDK_PATH}/components/libraries/mpu/"
    "${NRF5_SDK_PATH}/components/libraries/experimental_section_vars/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_ans_c/"
    "${NRF5_SDK_PATH}/components/libraries/slip/"
    "${NRF5_SDK_PATH}/components/libraries/delay/"
    "${NRF5_SDK_PATH}/components/libraries/csense_drv/"
    "${NRF5_SDK_PATH}/components/libraries/memobj/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_nus_c/"
    "${NRF5_SDK_PATH}/components/softdevice/common/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_ias/"
    "${NRF5_SDK_PATH}/components/libraries/usbd/class/hid/mouse/"
    "${NRF5_SDK_PATH}/components/libraries/low_power_pwm/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/conn_hand_parser/ble_oob_advdata_parser/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_dfu/"
    "${NRF5_SDK_PATH}/external/fprintf/"
    "${NRF5_SDK_PATH}/components/libraries/svc/"
    "${NRF5_SDK_PATH}/components/libraries/atomic/"
    "${NRF5_SDK_PATH}/components/"
    "${NRF5_SDK_PATH}/components/libraries/scheduler/"
    "${NRF5_SDK_PATH}/components/libraries/cli/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_lbs/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_hts/"
    "${NRF5_SDK_PATH}/components/libraries/crc16/"
    "${NRF5_SDK_PATH}/components/nfc/t4t_parser/apdu/"
    "${NRF5_SDK_PATH}/components/libraries/util/"
    "${NRF5_SDK_PATH}/components/libraries/usbd/class/cdc/"
    "${NRF5_SDK_PATH}/components/libraries/csense/"
    "${NRF5_SDK_PATH}/components/libraries/balloc/"
    "${NRF5_SDK_PATH}/components/libraries/ecc/"
    "${NRF5_SDK_PATH}/components/libraries/hardfault/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_cscs/"
    "${NRF5_SDK_PATH}/components/libraries/hci/"
    "${NRF5_SDK_PATH}/components/libraries/timer/"
    "${NRF5_SDK_PATH}/components/softdevice/s140/headers/"
    "${NRF5_SDK_PATH}/integration/nrfx/"
    "${NRF5_SDK_PATH}/components/nfc/t4t_parser/tlv/"
    "${NRF5_SDK_PATH}/components/libraries/sortlist/"
    "${NRF5_SDK_PATH}/components/libraries/spi_mngr/"
    "${NRF5_SDK_PATH}/components/libraries/led_softblink/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/conn_hand_parser/"
    "${NRF5_SDK_PATH}/components/libraries/sdcard/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/parser/record/"
    "${NRF5_SDK_PATH}/modules/nrfx/mdk/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_cts_c/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_nus/"
    "${NRF5_SDK_PATH}/components/libraries/twi_mngr/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_hids/"
    "${NRF5_SDK_PATH}/components/libraries/strerror/"
    "${NRF5_SDK_PATH}/components/libraries/crc32/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/connection_handover/ble_oob_advdata/"
    "${NRF5_SDK_PATH}/components/nfc/t2t_parser/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/connection_handover/ble_pair_msg/"
    "${NRF5_SDK_PATH}/components/libraries/usbd/class/audio/"
    "${NRF5_SDK_PATH}/components/libraries/sensorsim/"
    "${NRF5_SDK_PATH}/components/nfc/t4t_lib/"
    "${NRF5_SDK_PATH}/components/ble/peer_manager/"
    "${NRF5_SDK_PATH}/components/libraries/mem_manager/"
    "${NRF5_SDK_PATH}/components/libraries/ringbuf/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_tps/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/parser/message/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_dis/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/uri/"
    "${NRF5_SDK_PATH}/components/ble/nrf_ble_gatt/"
    "${NRF5_SDK_PATH}/components/ble/nrf_ble_qwr/"
    "${NRF5_SDK_PATH}/components/libraries/gfx/"
    "${NRF5_SDK_PATH}/components/libraries/button/"
    "${NRF5_SDK_PATH}/modules/nrfx/"
    "${NRF5_SDK_PATH}/components/libraries/twi_sensor/"
    "${NRF5_SDK_PATH}/integration/nrfx/legacy/"
    "${NRF5_SDK_PATH}/components/libraries/usbd/class/hid/kbd/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/connection_handover/ep_oob_rec/"
    "${NRF5_SDK_PATH}/external/segger_rtt/"
    "${NRF5_SDK_PATH}/components/libraries/atomic_fifo/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_lbs_c/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/connection_handover/ble_pair_lib/"
    "${NRF5_SDK_PATH}/components/libraries/crypto/"
    "${NRF5_SDK_PATH}/components/ble/ble_racp/"
    "${NRF5_SDK_PATH}/components/libraries/fds/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/launchapp/"
    "${NRF5_SDK_PATH}/components/libraries/atomic_flags/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_hrs/"
    "${NRF5_SDK_PATH}/components/ble/ble_services/ble_rscs/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/connection_handover/hs_rec/"
    "${NRF5_SDK_PATH}/components/libraries/usbd/"
    "${NRF5_SDK_PATH}/components/nfc/ndef/conn_hand_parser/ac_rec_parser/"
    "${NRF5_SDK_PATH}/components/libraries/stack_guard/"
    "${NRF5_SDK_PATH}/components/libraries/log/src/"
)

target_sources(nrf52840_xxaa
  PRIVATE
    "ble_cus.c"
    "${NRF5_SDK_PATH}/modules/nrfx/mdk/gcc_startup_nrf52840.S"
    "${NRF5_SDK_PATH}/modules/nrfx/mdk/system_nrf52840.c"
    "${NRF5_SDK_PATH}/components/libraries/log/src/nrf_log_backend_rtt.c"
    "${NRF5_SDK_PATH}/components/libraries/log/src/nrf_log_backend_serial.c"
    "${NRF5_SDK_PATH}/components/libraries/log/src/nrf_log_backend_uart.c"
    "${NRF5_SDK_PATH}/components/libraries/log/src/nrf_log_default_backends.c"
    "${NRF5_SDK_PATH}/components/libraries/log/src/nrf_log_frontend.c"
    "${NRF5_SDK_PATH}/components/libraries/log/src/nrf_log_str_formatter.c"
    "${NRF5_SDK_PATH}/components/libraries/button/app_button.c"
    "${NRF5_SDK_PATH}/components/libraries/util/app_error.c"
    "${NRF5_SDK_PATH}/components/libraries/util/app_error_handler_gcc.c"
    "${NRF5_SDK_PATH}/components/libraries/util/app_error_weak.c"
    "${NRF5_SDK_PATH}/components/libraries/scheduler/app_scheduler.c"
    "${NRF5_SDK_PATH}/components/libraries/timer/app_timer.c"
    "${NRF5_SDK_PATH}/components/libraries/util/app_util_platform.c"
    "${NRF5_SDK_PATH}/components/libraries/crc16/crc16.c"
    "${NRF5_SDK_PATH}/components/libraries/fds/fds.c"
    "${NRF5_SDK_PATH}/components/libraries/hardfault/hardfault_implementation.c"
    "${NRF5_SDK_PATH}/components/libraries/util/nrf_assert.c"
    "${NRF5_SDK_PATH}/components/libraries/atomic_fifo/nrf_atfifo.c"
    "${NRF5_SDK_PATH}/components/libraries/atomic_flags/nrf_atflags.c"
    "${NRF5_SDK_PATH}/components/libraries/atomic/nrf_atomic.c"
    "${NRF5_SDK_PATH}/components/libraries/balloc/nrf_balloc.c"
    "${NRF5_SDK_PATH}/external/fprintf/nrf_fprintf.c"
    "${NRF5_SDK_PATH}/external/fprintf/nrf_fprintf_format.c"
    "${NRF5_SDK_PATH}/components/libraries/fstorage/nrf_fstorage.c"
    "${NRF5_SDK_PATH}/components/libraries/fstorage/nrf_fstorage_sd.c"
    "${NRF5_SDK_PATH}/components/libraries/memobj/nrf_memobj.c"
    "${NRF5_SDK_PATH}/components/libraries/pwr_mgmt/nrf_pwr_mgmt.c"
    "${NRF5_SDK_PATH}/components/libraries/ringbuf/nrf_ringbuf.c"
    "${NRF5_SDK_PATH}/components/libraries/experimental_section_vars/nrf_section_iter.c"
    "${NRF5_SDK_PATH}/components/libraries/strerror/nrf_strerror.c"
    "${NRF5_SDK_PATH}/components/libraries/sensorsim/sensorsim.c"
    "${NRF5_SDK_PATH}/components/boards/boards.c"
    "${NRF5_SDK_PATH}/integration/nrfx/legacy/nrf_drv_clock.c"
    "${NRF5_SDK_PATH}/integration/nrfx/legacy/nrf_drv_uart.c"
    "${NRF5_SDK_PATH}/modules/nrfx/soc/nrfx_atomic.c"
    "${NRF5_SDK_PATH}/modules/nrfx/drivers/src/nrfx_clock.c"
    "${NRF5_SDK_PATH}/modules/nrfx/drivers/src/nrfx_gpiote.c"
    "${NRF5_SDK_PATH}/modules/nrfx/drivers/src/prs/nrfx_prs.c"
    "${NRF5_SDK_PATH}/modules/nrfx/drivers/src/nrfx_uart.c"
    "${NRF5_SDK_PATH}/modules/nrfx/drivers/src/nrfx_uarte.c"
    "${NRF5_SDK_PATH}/components/libraries/bsp/bsp.c"
    "${NRF5_SDK_PATH}/components/libraries/bsp/bsp_btn_ble.c"
    "${NRF5_SDK_PATH}/external/segger_rtt/SEGGER_RTT.c"
    "${NRF5_SDK_PATH}/external/segger_rtt/SEGGER_RTT_Syscalls_GCC.c"
    "${NRF5_SDK_PATH}/external/segger_rtt/SEGGER_RTT_printf.c"
    "${NRF5_SDK_PATH}/components/ble/peer_manager/auth_status_tracker.c"
    "${NRF5_SDK_PATH}/components/ble/common/ble_advdata.c"
    "${NRF5_SDK_PATH}/components/ble/ble_advertising/ble_advertising.c"
    "${NRF5_SDK_PATH}/components/ble/common/ble_conn_params.c"
    "${NRF5_SDK_PATH}/components/ble/common/ble_conn_state.c"
    "${NRF5_SDK_PATH}/components/ble/common/ble_srv_common.c"
    "${NRF5_SDK_PATH}/components/ble/peer_manager/gatt_cache_manager.c"
    "${NRF5_SDK_PATH}/components/ble/peer_manager/gatts_cache_manager.c"
    "${NRF5_SDK_PATH}/components/ble/peer_manager/id_manager.c"
    "${NRF5_SDK_PATH}/components/ble/nrf_ble_gatt/nrf_ble_gatt.c"
    "${NRF5_SDK_PATH}/components/ble/nrf_ble_qwr/nrf_ble_qwr.c"
    "${NRF5_SDK_PATH}/components/ble/peer_manager/peer_data_storage.c"
    "${NRF5_SDK_PATH}/components/ble/peer_manager/peer_database.c"
    "${NRF5_SDK_PATH}/components/ble/peer_manager/peer_id.c"
    "${NRF5_SDK_PATH}/components/ble/peer_manager/peer_manager.c"
    "${NRF5_SDK_PATH}/components/ble/peer_manager/peer_manager_handler.c"
    "${NRF5_SDK_PATH}/components/ble/peer_manager/pm_buffer.c"
    "${NRF5_SDK_PATH}/components/ble/peer_manager/security_dispatcher.c"
    "${NRF5_SDK_PATH}/components/ble/peer_manager/security_manager.c"
    "${NRF5_SDK_PATH}/external/utf_converter/utf.c"
    "${NRF5_SDK_PATH}/components/softdevice/common/nrf_sdh.c"
    "${NRF5_SDK_PATH}/components/softdevice/common/nrf_sdh_ble.c"
    "${NRF5_SDK_PATH}/components/softdevice/common/nrf_sdh_soc.c"
)

set(OPT -O3 -g3)

target_compile_options(nrf52840_xxaa
  PRIVATE
    "${OPT}"
    -mcpu=cortex-m4
    -mthumb -mabi=aapcs
    -mfloat-abi=hard -mfpu=fpv4-sp-d16
    # keep every function in a separate section, this allows linker to discard unused ones
    -ffunction-sections -fdata-sections -fno-strict-aliasing
    -fno-builtin -fshort-enums
    # MODIFIED 21.01.2023 - Marek Ištok
    # -Wall -Werror
    -Wall
)

target_compile_definitions(nrf52840_xxaa
  PRIVATE
    -D__HEAP_SIZE=8192
    -D__STACK_SIZE=8192
    -DBOARD_PCA10056
    -DCONFIG_GPIO_AS_PINRESET
    -DFLOAT_ABI_HARD
    -DNRF52840_XXAA
    -DNRF_SD_BLE_API_VERSION=6
    -DS140
    -DSOFTDEVICE_PRESENT
    -DSWI_DISABLE0
)

# make sdk_config.h import app_config.h
target_compile_definitions(nrf52840_xxaa PRIVATE USE_APP_CONFIG)

target_link_options(nrf52840_xxaa
  PRIVATE
    "${OPT}"
    -mthumb -mabi=aapcs
    -L "${NRF5_SDK_PATH}/modules/nrfx/mdk"
    -T "${CMAKE_SOURCE_DIR}/ble_app_template_gcc_nrf52.ld"
    -mcpu=cortex-m4
    # let linker dump unused sections
    -mfloat-abi=hard -mfpu=fpv4-sp-d16
    -Wl,--gc-sections
    # use newlib in nano version
    --specs=nano.specs
)

target_link_libraries(nrf52840_xxaa
  PRIVATE
    -lc -lnosys -lm
)

# Print size information after build
add_custom_command(TARGET nrf52840_xxaa POST_BUILD
  COMMAND ${CMAKE_SIZE_BIN} "${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/nrf52840_xxaa"
)

# Targets for creating Intel HEX and binary executable forms
add_custom_target(hex DEPENDS nrf52840_xxaa
  COMMAND
    ${CMAKE_OBJCOPY_BIN} -O ihex
      "${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/nrf52840_xxaa"
      "${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/nrf52840_xxaa.hex"
)
add_custom_target(bin DEPENDS nrf52840_xxaa
  COMMAND
    ${CMAKE_OBJCOPY_BIN} -O binary
      "${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/nrf52840_xxaa"
      "${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/nrf52840_xxaa.bin"
)