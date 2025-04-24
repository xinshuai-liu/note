grpc

git clone -b v1.34.0 https://gitee.com/mirrors/grpc-framework.git grpc

修改.gitmodules

[submodule "third_party/zlib"]
    path = third_party/zlib
    #url = https://github.com/madler/zlib
    url = https://gitee.com/mirrors/zlib.git
    # When using CMake to build, the zlib submodule ends up with a
    # generated file that makes Git consider the submodule dirty. This
    # state can be ignored for day-to-day development on gRPC.
    ignore = dirty
[submodule "third_party/protobuf"]
    path = third_party/protobuf
    #url = https://github.com/google/protobuf.git
    url = https://gitee.com/local-grpc/protobuf.git
[submodule "third_party/googletest"]
    path = third_party/googletest
    #url = https://github.com/google/googletest.git
    url = https://gitee.com/local-grpc/googletest.git
[submodule "third_party/benchmark"]
    path = third_party/benchmark
    #url = https://github.com/google/benchmark
    url = https://gitee.com/mirrors/google-benchmark.git
[submodule "third_party/boringssl-with-bazel"]
    path = third_party/boringssl-with-bazel
    #url = https://github.com/google/boringssl.git
    url = https://gitee.com/mirrors/boringssl.git
[submodule "third_party/re2"]
    path = third_party/re2
    #url = https://github.com/google/re2.git
    url = https://gitee.com/local-grpc/re2.git
[submodule "third_party/cares/cares"]
    path = third_party/cares/cares
    #url = https://github.com/c-ares/c-ares.git
    url = https://gitee.com/mirrors/c-ares.git
    branch = cares-1_12_0
[submodule "third_party/bloaty"]
    path = third_party/bloaty
    #url = https://github.com/google/bloaty.git
    url = https://gitee.com/local-grpc/bloaty.git
[submodule "third_party/abseil-cpp"]
    path = third_party/abseil-cpp
    #url = https://github.com/abseil/abseil-cpp.git
    url = https://gitee.com/mirrors/abseil-cpp.git
    branch = lts_2020_02_25
[submodule "third_party/envoy-api"]
    path = third_party/envoy-api
    #url = https://github.com/envoyproxy/data-plane-api.git
    url = https://gitee.com/local-grpc/data-plane-api.git
[submodule "third_party/googleapis"]
    path = third_party/googleapis
    #url = https://github.com/googleapis/googleapis.git
    url = https://gitee.com/mirrors/googleapis.git
[submodule "third_party/protoc-gen-validate"]
    path = third_party/protoc-gen-validate
    #url = https://github.com/envoyproxy/protoc-gen-validate.git
    url = https://gitee.com/local-grpc/protoc-gen-validate.git
[submodule "third_party/udpa"]
    path = third_party/udpa
    #url = https://github.com/cncf/udpa.git
    url = https://gitee.com/local-grpc/udpa.git
[submodule "third_party/libuv"]
    path = third_party/libuv
    #url = https://github.com/libuv/libuv.git
    url = https://gitee.com/mirrors/libuv.git


cd grpc
git submodule update --init

(可能需要 git config --global --add safe.directory /grpc)

cd grpc
mkdir build
cd build
// 指定安装路径 /usr/local 
cmake -DCMAKE_INSTALL_PREFIX=/usr/local ..
make -j2
(可能有错误
vim /grpc/third_party/abseil-cpp/absl/synchronization/internal/graphcycles.cc
#include <limits>

vim /grpc/third_party/abseil-cpp/absl/debugging/failure_signal_handler.cc
size_t stack_size = (std::max(SIGSTKSZ, static_cast<long int>(65536)) + page_mask) & ~page_mask;
)
sudo make install

#测试 进入grpc文件夹下
cd examples/cpp/helloworld
mkdir build
cd build
cmake ..
make -j8
cd grpc/examples/cpp/helloworld/build/
./greeter_server 
./greeter_client