workspace(name = "scalapb-zio-grpc")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "bazel_skylib",
    sha256 = "1c531376ac7e5a180e0237938a2536de0c54d93f5c278634818e0efc952dd56c",
    url = "https://mirror.bazel.build/github.com/bazelbuild/bazel-skylib/releases/download/1.0.3/bazel-skylib-1.0.3.tar.gz",
)

http_archive(
    name = "rules_jvm_external",
    sha256 = "31701ad93dbfe544d597dbe62c9a1fdd76d81d8a9150c2bf1ecf928ecdf97169",
    strip_prefix = "rules_jvm_external-4.0",
    url = "https://github.com/bazelbuild/rules_jvm_external/archive/4.0.zip",
)

http_archive(
    name = "rules_proto",
    sha256 = "8e7d59a5b12b233be5652e3d29f42fba01c7cbab09f6b3a8d0a57ed6d1e9a0da",
    strip_prefix = "rules_proto-7e4afce6fe62dbff0a4a03450143146f9f2d7488",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_proto/archive/7e4afce6fe62dbff0a4a03450143146f9f2d7488.tar.gz",
        "https://github.com/bazelbuild/rules_proto/archive/7e4afce6fe62dbff0a4a03450143146f9f2d7488.tar.gz",
    ],
)

http_archive(
    name = "io_bazel_rules_scala",
    sha256 = "8887906c9698a63f7ebf30498050fee695d7fdc70b0ee084fece549cbe922159",
    strip_prefix = "rules_scala-c9cc7c261d3d740eb91ef8ef048b7cd2229d12ec",
    url = "https://github.com/bazelbuild/rules_scala/archive/c9cc7c261d3d740eb91ef8ef048b7cd2229d12ec.zip",
)

load("@rules_jvm_external//:defs.bzl", "maven_install")
load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")

rules_proto_dependencies()

rules_proto_toolchains()

load("@io_bazel_rules_scala//:scala_config.bzl", "scala_config")

scala_config(scala_version = "2.13.x")

load("@io_bazel_rules_scala//scala:scala.bzl", "scala_repositories")

scala_repositories()

maven_install(
    artifacts = [
        "com.thesamet.scalapb:scalapb-runtime_2.13:0.11.2",
        "com.thesamet.scalapb:scalapb-runtime-grpc_2.13:0.11.2",
        "com.thesamet.scalapb:compilerplugin_2.13:0.11.2",
        "com.thesamet.scalapb:protoc-bridge_2.13:0.9.2",
        "com.thesamet.scalapb:protoc-gen_2.13:0.9.2",
        "com.thesamet.scalapb:lenses_2.13:0.11.2",
        "com.thesamet.scalapb.zio-grpc:zio-grpc-codegen_2.13:0.5.0",
        "com.thesamet.scalapb.zio-grpc:zio-grpc-core_2.13:0.5.0",
        "dev.zio:zio_2.13:1.0.7",
        "dev.zio:izumi-reflect_2.13:1.1.1",
        "dev.zio:izumi-reflect-thirdparty-boopickle-shaded_2.13:1.1.1",
        "io.grpc:grpc-api:1.37.0",
        "io.grpc:grpc-core:1.37.0",
        "io.grpc:grpc-stub:1.37.0",
        "io.grpc:grpc-context:1.37.0",
        "io.grpc:grpc-services:1.37.0",
        "io.grpc:grpc-protobuf:1.37.0",
        "io.grpc:grpc-protobuf-lite:1.37.0",
    ],
    repositories = [
        "https://maven.google.com",
        "https://repo1.maven.org/maven2",
    ],
)

load("@io_bazel_rules_scala//scala:toolchains.bzl", "scala_register_toolchains")

scala_register_toolchains()

register_toolchains("//:scala_proto_deps_toolchain")

register_toolchains("//:scalapb_zio_grpc_toolchain")
