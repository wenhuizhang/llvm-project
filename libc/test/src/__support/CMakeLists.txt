add_libc_testsuite(libc_support_unittests)

add_libc_unittest(
  endian_test
  SUITE
    libc_support_unittests
  SRCS
    endian_test.cpp
  DEPENDS
    libc.src.__support.common
)

add_libc_unittest(
  high_precision_decimal_test
  SUITE
    libc_support_unittests
  SRCS
  high_precision_decimal_test.cpp
  DEPENDS
    libc.src.__support.high_precision_decimal
)

add_libc_unittest(
  str_to_float_test
  SUITE
    libc_support_unittests
  SRCS
    str_to_float_test.cpp
  DEPENDS
    libc.src.__support.str_conv_utils
)

add_executable(
  libc_str_to_float_comparison_test
  str_to_float_comparison_test.cpp
)

target_link_libraries(libc_str_to_float_comparison_test
  PRIVATE
    llvmlibc
)

set(float_test_file ${CMAKE_CURRENT_SOURCE_DIR}/str_to_float_comparison_data.txt)

add_custom_command(TARGET libc_str_to_float_comparison_test
                   POST_BUILD
                   COMMAND $<TARGET_FILE:libc_str_to_float_comparison_test> ${float_test_file}
                   DEPENDS ${float_test_file}
                   COMMENT "Test the strtof and strtod implementations against precomputed results." 
                   VERBATIM)
