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

option(BUILD_STATIC "build a static executable" OFF)
if (BUILD_STATIC)
  add_library(eb STATIC IMPORTED)
  if (APPLE)
    set_target_properties(eb PROPERTIES IMPORTED_LOCATION /usr/local/lib/libeb.a)
  else(APPLE)
    set_target_properties(eb PROPERTIES IMPORTED_LOCATION /usr/lib/x86_64-linux-gnu/libeb.a)
    set(CMAKE_FIND_LIBRARY_SUFFIXES ".a")
    set(BUILD_SHARED_LIBRARIES OFF)
    set(CMAKE_EXE_LINKER_FLAGS "-static")
  endif(APPLE)
endif(BUILD_STATIC)

if (APPLE)
  target_link_libraries(eb iconv)
endif(APPLE)

add_executable(eplkup ${SOURCE_FILES})
target_link_libraries(eplkup eb z)
install (TARGETS eplkup DESTINATION bin)
