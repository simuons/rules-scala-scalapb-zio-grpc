load("@io_bazel_rules_scala//scala:providers.bzl", "declare_deps_provider")
load("@io_bazel_rules_scala//scala:scala_toolchain.bzl", "scala_toolchain")
load("@io_bazel_rules_scala//scala_proto:scala_proto_toolchain.bzl", "scala_proto_deps_toolchain", "scala_proto_toolchain")
load("@io_bazel_rules_scala//scala_proto:scala_proto.bzl", "scala_proto_library")

package(default_visibility = ["//visibility:public"])

declare_deps_provider(
    name = "scala_compile_classpath_provider",
    deps_id = "scala_compile_classpath",
    deps = [
        "@maven//:org_scala_lang_scala_compiler",
        "@maven//:org_scala_lang_scala_library",
        "@maven//:org_scala_lang_scala_reflect",
    ],
)

declare_deps_provider(
    name = "scala_library_classpath_provider",
    deps_id = "scala_library_classpath",
    deps = [
        "@maven//:org_scala_lang_scala_library",
        "@maven//:org_scala_lang_scala_reflect",
    ],
)

declare_deps_provider(
    name = "scala_macro_classpath_provider",
    deps_id = "scala_macro_classpath",
    deps = [
        "@maven//:org_scala_lang_scala_library",
        "@maven//:org_scala_lang_scala_reflect",
    ],
)

declare_deps_provider(
    name = "scala_xml_provider",
    deps_id = "scala_xml",
    deps = [
        "@maven//:org_scala_lang_modules_scala_xml_2_12",
    ],
)

declare_deps_provider(
    name = "parser_combinators_provider",
    deps_id = "parser_combinators",
    deps = [
        "@maven//:org_scala_lang_modules_scala_parser_combinators_2_12",
    ],
)

scala_toolchain(
    name = "scala_toolchain_def",
    dep_providers = [
        ":scala_compile_classpath_provider",
        ":scala_library_classpath_provider",
        ":scala_macro_classpath_provider",
        ":scala_xml_provider",
        ":parser_combinators_provider",
    ],
    scalacopts = [],
)

toolchain(
    name = "scala_toolchain",
    toolchain = ":scala_toolchain_def",
    toolchain_type = "@io_bazel_rules_scala//scala:toolchain_type",
)

declare_deps_provider(
    name = "scalapb_worker_deps_provider",
    deps_id = "scalapb_worker_deps",
    deps = [
        "@com_google_protobuf//:protobuf_java",
        "@maven//:com_thesamet_scalapb_compilerplugin_2_12",
        "@maven//:com_thesamet_scalapb_protoc_bridge_2_12",
    ],
)

declare_deps_provider(
    name = "scalapb_compile_deps_provider",
    deps_id = "scalapb_compile_deps",
    deps = [
        "@com_google_protobuf//:protobuf_java",
        "@maven//:com_thesamet_scalapb_lenses_2_12",
        "@maven//:com_thesamet_scalapb_scalapb_runtime_2_12",
        "@maven//:com_thesamet_scalapb_scalapb_runtime_grpc_2_12",
        "@maven//:com_thesamet_scalapb_zio_grpc_zio_grpc_core_2_12",
        "@maven//:dev_zio_izumi_reflect_2_12",
        "@maven//:dev_zio_izumi_reflect_thirdparty_boopickle_shaded_2_12",
        "@maven//:dev_zio_zio_2_12",
        "@maven//:io_grpc_grpc_api",
        "@maven//:io_grpc_grpc_context",
        "@maven//:io_grpc_grpc_core",
        "@maven//:io_grpc_grpc_protobuf",
        "@maven//:io_grpc_grpc_stub",
        "@maven//:org_scala_lang_scala_compiler",
        "@maven//:org_scala_lang_scala_library",
        "@maven//:org_scala_lang_scala_reflect",
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
    name = "scala_proto_zio_grpc_toolchain_def",
    extra_generator_dependencies = [
        "@maven//:com_thesamet_scalapb_zio_grpc_zio_grpc_codegen_2_12",
    ],
    main_generator = "scalapb.ScalaPbCodeGenerator",
    named_generators = {
        "zio": "scalapb.zio_grpc.ZioCodeGenerator",
    },
    with_grpc = True,
)

toolchain(
    name = "scala_proto_zio_grpc_toolchain",
    toolchain = ":scala_proto_zio_grpc_toolchain_def",
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
