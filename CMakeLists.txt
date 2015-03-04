cmake_minimum_required(VERSION 2.8.4)
project(eplkup)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Werror")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_LIST_DIR}/out/")

set(SOURCE_FILES
  base64.c
  base64.h
  eplkup.c
  eplkup_data.c
  eplkup_data.h
  eplkup_font.c
  eplkup_font.h
  eplkup_gaiji.c
  eplkup_gaiji.h
  eplkup_hook_handler.c
  eplkup_hook_handler.h
  eplkup_utils.c
  eplkup_utils.h
  gaiji_table_chujiten.c
  gaiji_table_daijirin.c
  gaiji_table_daijisen.c
  gaiji_table_genius.c
  gaiji_table_kojien.c
  gaiji_table_meikyojj.c
  gaiji_table_meikyou.c
  gaiji_table_snmkg99.c
  gaiji_table_wadai5.c)

add_executable(eplkup ${SOURCE_FILES})
target_link_libraries(eplkup eb iconv)
install (TARGETS eplkup DESTINATION bin)
