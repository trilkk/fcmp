cmake_minimum_required(VERSION 3.1)
set(CMAKE_CONFIGURATION_TYPES "Debug;Release")
project(fcmp)

enable_language(C)
enable_language(CXX)

include("defaults.cmake")

find_boost("filesystem" "program_options" "system" "thread")
find_threads()

output_flags("DEBUG" on)

include_directories("${PROJECT_SOURCE_DIR}/src")

add_executable(fcmp
  "src/arithmetic_coder.hpp"
  "src/arithmetic_decoder.cpp"
  "src/arithmetic_decoder.hpp"
  "src/arithmetic_encoder.cpp"
  "src/arithmetic_encoder.hpp"
  "src/bit_file.cpp"
  "src/bit_file.hpp"
  "src/common.cpp"
  "src/common.hpp"
  "src/compressor.cpp"
  "src/compressor.hpp"
  "src/compressor_state.cpp"
  "src/compressor_state.hpp"
  "src/compressor_thread.cpp"
  "src/compressor_thread.hpp"
  "src/data_bits.cpp"
  "src/data_bits.hpp"
  "src/data_bits_reader.cpp"
  "src/data_bits_reader.hpp"
  "src/data_bits_state.cpp"
  "src/data_bits_state.hpp"
  "src/data_compressed.cpp"
  "src/data_compressed.hpp"
  "src/data_compressed_reader.cpp"
  "src/data_compressed_reader.hpp"
  "src/filesystem.hpp"
  "src/main.cpp"
  "src/model.cpp"
  "src/model.hpp"
  "src/prediction.hpp"
  "src/predictor_key.cpp"
  "src/predictor_key.hpp"
  "src/predictor_value.cpp"
  "src/predictor_value.hpp"
  "src/probability.hpp"
  "src/threading.hpp")
if(${MSVC})
  target_link_libraries(fcmp "WINMM")
else()
  target_link_libraries(fcmp "${BOOST_FILESYSTEM_LIBRARY}")
  target_link_libraries(fcmp "${BOOST_PROGRAM_OPTIONS_LIBRARY}")
  target_link_libraries(fcmp "${BOOST_SYSTEM_LIBRARY}")
endif()
target_link_libraries(fcmp "${THREADS_LIBRARY}")
