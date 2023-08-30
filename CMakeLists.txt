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
if(WIN32)
    set(bsoncxx_DIR "D:/mongo-driver-cxx/mongo-cxx-driver/lib/cmake/bsoncxx-3.8.0")
    set(mongocxx_DIR "D:/mongo-driver-cxx/mongo-cxx-driver/lib/cmake/mongocxx-3.8.0")
endif()
find_package(bsoncxx REQUIRED)
find_package(mongocxx REQUIRED)

# Add your CUDA source files and other source files
set(SOURCES
    mongoandcuda.cpp
    mongoandcuda.h
    asyncAPI.cu
)

# Add source to this project's executable.
add_executable(mgCudaExec ${SOURCES})

if(WIN32)
    # Windows specific settings
    # set third part depedency
    include_directories("D:/cuda12/example/cuda-samples-master/Common")

    file(GLOB CUDA_LIBS "D:/cuda12/example/cuda-samples-master/Common/lib/x64/*.lib")
    target_link_libraries(mgCudaExec ${CUDA_LIBS})
else()
    # Link against the found libraries
    target_link_libraries(mgCudaExec "/usr/local/lib/libbsoncxx.so") # ${BSONCXX_LIBRARIES})
    target_link_libraries(mgCudaExec "/usr/local/lib/libmongocxx.so") # ${MONGOCXX_LIBRARIES})

    # Add the include directories
    target_include_directories(mgCudaExec PRIVATE "/usr/local/include/bsoncxx/v_noabi") # ${BSONCXX_INCLUDE_DIRS})
    target_include_directories(mgCudaExec PRIVATE "/usr/local/include/mongocxx/v_noabi") # ${MONGOCXX_INCLUDE_DIRS}) 

    # set third part depedency
    include_directories("/root/dependency/cuda12/cuda-samples-master/Common")
endif()
