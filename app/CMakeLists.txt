cmake_minimum_required(VERSION 3.4.1)

add_library(
             native-lib
             SHARED
             src/main/cpp/native-lib.cpp
             )
find_library(
          android-lib
          android
          )

include(AndroidNdkModules)
android_ndk_import_module_cpufeatures()

add_library(
    caffe2
    STATIC
    IMPORTED
    )
set_target_properties(
    caffe2
    PROPERTIES IMPORTED_LOCATION
    ${CMAKE_CURRENT_LIST_DIR}/src/main/jniLibs/${ANDROID_ABI}/libcaffe2.a
    )

add_library(
    caffe2_protos
    STATIC
    IMPORTED
    )
set_target_properties(
    caffe2_protos
    PROPERTIES IMPORTED_LOCATION
    ${CMAKE_CURRENT_LIST_DIR}/src/main/jniLibs/${ANDROID_ABI}/libcaffe2_protos.a
    )

add_library(
    nnpack
    STATIC
    IMPORTED
    )
set_target_properties(
    nnpack
    PROPERTIES IMPORTED_LOCATION
    ${CMAKE_CURRENT_LIST_DIR}/src/main/jniLibs/${ANDROID_ABI}/libnnpack.a
    )

add_library(
    cpuinfo
    STATIC
    IMPORTED
    )
set_target_properties(
    cpuinfo
    PROPERTIES IMPORTED_LOCATION
    ${CMAKE_CURRENT_LIST_DIR}/src/main/jniLibs/${ANDROID_ABI}/libcpuinfo.a
    )

add_library(
    nnpack_reference_layers
    STATIC
    IMPORTED
    )
set_target_properties(
    nnpack_reference_layers
    PROPERTIES IMPORTED_LOCATION
    ${CMAKE_CURRENT_LIST_DIR}/src/main/jniLibs/${ANDROID_ABI}/libnnpack_reference_layers.a
    )

add_library(
    nomnigraph
    STATIC
    IMPORTED
    )
set_target_properties(
    nomnigraph
    PROPERTIES IMPORTED_LOCATION
    ${CMAKE_CURRENT_LIST_DIR}/src/main/jniLibs/${ANDROID_ABI}/libnomnigraph.a
    )

add_library(
    onnx
    STATIC
    IMPORTED
    )
set_target_properties(
    onnx
    PROPERTIES IMPORTED_LOCATION
    ${CMAKE_CURRENT_LIST_DIR}/src/main/jniLibs/${ANDROID_ABI}/libonnx.a
    )

add_library(
    onnx_proto
    STATIC
    IMPORTED
    )
set_target_properties(
    onnx_proto
    PROPERTIES IMPORTED_LOCATION
    ${CMAKE_CURRENT_LIST_DIR}/src/main/jniLibs/${ANDROID_ABI}/libonnx_proto.a
    )

add_library(
    protobuf
    STATIC
    IMPORTED
    )
set_target_properties(
    protobuf
    PROPERTIES IMPORTED_LOCATION
    ${CMAKE_CURRENT_LIST_DIR}/src/main/jniLibs/${ANDROID_ABI}/libprotobuf.a
    )

add_library(
    protobuf-lite
    STATIC
    IMPORTED
    )
set_target_properties(
    protobuf-lite
    PROPERTIES IMPORTED_LOCATION
    ${CMAKE_CURRENT_LIST_DIR}/src/main/jniLibs/${ANDROID_ABI}/libprotobuf-lite.a
    )

add_library(
    pthreadpool
    STATIC
    IMPORTED
    )
set_target_properties(
    pthreadpool
    PROPERTIES IMPORTED_LOCATION
    ${CMAKE_CURRENT_LIST_DIR}/src/main/jniLibs/${ANDROID_ABI}/libpthreadpool.a
    )



include_directories( src/main/cpp )

find_library(
     log-lib
     log
     )

target_link_libraries(
                       native-lib
                       -Wl,--whole-archive
                       caffe2
                       caffe2_protos
                       nnpack
                       nnpack_reference_layers
                       nomnigraph
                       onnx
                       onnx_proto
                       protobuf
                       cpuinfo
                       #pthreadpool
                       -Wl,--no-whole-archive
                       ${log-lib}
                       ${android-lib})