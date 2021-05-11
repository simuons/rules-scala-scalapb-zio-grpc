load("@io_bazel_rules_scala//scala:providers.bzl", "declare_deps_provider")
load("@io_bazel_rules_scala//scala_proto:scala_proto_toolchain.bzl", "scala_proto_deps_toolchain", "scala_proto_toolchain")
load("@io_bazel_rules_scala//scala_proto:scala_proto.bzl", "scala_proto_library")

package(default_visibility = ["//visibility:public"])

declare_deps_provider(
    name = "scalapb_worker_deps_provider",
    deps_id = "scalapb_worker_deps",
    deps = [
        "@com_google_protobuf//:protobuf_java",
        "@maven//:com_thesamet_scalapb_compilerplugin_2_13",
        "@maven//:com_thesamet_scalapb_protoc_bridge_2_13",
    ],
)

declare_deps_provider(
    name = "scalapb_compile_deps_provider",
    deps_id = "scalapb_compile_deps",
    deps = [
        "@com_google_protobuf//:protobuf_java",
        "@io_bazel_rules_scala_scala_compiler",
        "@io_bazel_rules_scala_scala_library",
        "@io_bazel_rules_scala_scala_reflect",
        "@maven//:com_thesamet_scalapb_lenses_2_13",
        "@maven//:com_thesamet_scalapb_scalapb_runtime_2_13",
        "@maven//:com_thesamet_scalapb_scalapb_runtime_grpc_2_13",
        "@maven//:com_thesamet_scalapb_zio_grpc_zio_grpc_core_2_13",
        "@maven//:dev_zio_izumi_reflect_2_13",
        "@maven//:dev_zio_izumi_reflect_thirdparty_boopickle_shaded_2_13",
        "@maven//:dev_zio_zio_2_13",
        "@maven//:io_grpc_grpc_api",
        "@maven//:io_grpc_grpc_context",
        "@maven//:io_grpc_grpc_core",
        "@maven//:io_grpc_grpc_protobuf",
        "@maven//:io_grpc_grpc_stub",
    ],
)

declare_deps_provider(
    name = "scalapb_grpc_deps_provider",
    deps_id = "scalapb_grpc_deps",
    deps = [],
)

scala_proto_deps_toolchain(
    name = "scala_proto_deps_toolchain_def",
    dep_providers = [
        ":scalapb_worker_deps_provider",
        ":scalapb_compile_deps_provider",
        ":scalapb_grpc_deps_provider",
    ],
)

toolchain(
    name = "scala_proto_deps_toolchain",
    toolchain = ":scala_proto_deps_toolchain_def",
    toolchain_type = "@io_bazel_rules_scala//scala_proto:deps_toolchain_type",
)

scala_proto_toolchain(
    name = "scalapb_zio_grpc_toolchain_def",
    extra_generator_dependencies = [
        "@maven//:com_thesamet_scalapb_zio_grpc_zio_grpc_codegen_2_13",
    ],
    main_generator = "scalapb.ScalaPbCodeGenerator",
    named_generators = {
        "zio": "scalapb.zio_grpc.ZioCodeGenerator",
    },
    with_grpc = True,
)

toolchain(
    name = "scalapb_zio_grpc_toolchain",
    toolchain = ":scalapb_zio_grpc_toolchain_def",
    toolchain_type = "@io_bazel_rules_scala//scala_proto:toolchain_type",
)

proto_library(
    name = "proto",
    srcs = ["example.proto"],
)

scala_proto_library(
    name = "scala",
    deps = [":proto"],
)
