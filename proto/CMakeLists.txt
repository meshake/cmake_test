find_package(Protobuf REQUIRED)
conan_define_targets()

protobuf_generate_cpp(PROTO_SRCS PROTO_HDRS sensor.proto)

add_executable(test-proto sensor.cpp ${PROTO_SRCS} ${PROTO_HDRS})
target_compile_options(test-proto PRIVATE -D_GLIBCXX_USE_CXX11_ABI=0)
target_link_libraries(test-proto PRIVATE CONAN_PKG::protobuf)
target_include_directories(test-proto PRIVATE ${CMAKE_BINARY_DIR}/proto)
