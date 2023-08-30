# CMakeList.txt : CMake project for mongoandcuda, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

project ("BurninG" LANGUAGES CXX CUDA)

# TODO: Add tests and install targets if needed.

# Find the CUDA package
# find_package(CUDA REQUIRED)
set(CMAKE_CUDA_ARCHITECTURES 75)

# Find the MONGOCXX package
set(bsoncxx_DIR "D:/mongo-driver-cxx/mongo-cxx-driver/lib/cmake/bsoncxx-3.8.0")
find_package(bsoncxx REQUIRED)

set(mongocxx_DIR "D:/mongo-driver-cxx/mongo-cxx-driver/lib/cmake/mongocxx-3.8.0")
find_package(mongocxx REQUIRED)

# Add your CUDA source files and other source files
set(SOURCES
    mongoandcuda.cpp
    mongoandcuda.h
    asyncAPI.cu
)

# Set CUDA flags and properties
# set(CUDA_NVCC_FLAGS "${CUDA_NVCC_FLAGS} -arch=compute_75 -code=sm_75")  # Adjust compute capability as needed

# Add source to this project's executable.
add_executable(mgCudaExec ${SOURCES})

# set third part depedency
include_directories("D:/cuda12/example/cuda-samples-master/Common")
target_link_libraries(mgCudaExec "D:/cuda12/example/cuda-samples-master/Common/lib/x64/*.lib")
