find_package(CUDA)

set(PROJ_INCLUDE      "../../")
set(mgpu_INCLUDE_DIRS "../../externals/moderngpu/include")
set(mgpu_SOURCE_DIRS  "../../externals/moderngpu/src")
set(cub_INCLUDE_DIRS  "../../externals/cub")

if(mgpu_INCLUDE_DIRS)
  include_directories(${mgpu_INCLUDE_DIRS} ${PROJ_INCLUDE} ${cub_INCLUDE_DIRS})
else()
  message(SEND_ERROR "Modern GPU include directory not set.")
endif()

set (mgpu_SOURCE_FILES
  ${mgpu_SOURCE_DIRS}/mgpucontext.cu
  ${mgpu_SOURCE_DIRS}/mgpuutil.cpp)
set( CMAKE_CXX_FLAGS "-std=c++11" )

cuda_add_executable(simple_example
  simple_example.cu
  ../../gunrock/util/test_utils.cu
  ../../gunrock/util/error_utils.cu
  ${mgpu_SOURCE_FILES}
  OPTIONS ${GENCODE} ${VERBOSE_PTXAS})
