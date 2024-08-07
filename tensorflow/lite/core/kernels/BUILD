load("//tensorflow:tensorflow.default.bzl", "get_compatible_with_portable")
load("//tensorflow/lite:build_def.bzl", "tflite_copts", "tflite_self_contained_libs_test_suite")
load("//tensorflow/lite/core:special_rules.bzl", "builtin_ops_visibility_allowlist")

package(
    # copybara:uncomment default_applicable_licenses = ["//tensorflow:license"],
    licenses = ["notice"],
)

exports_files(
    srcs = [
        "builtin_op_kernels.h",
        "register.h",
    ],
    visibility = [
        "//research/drishti/benchmarking/async:__subpackages__",
        "//tensorflow/lite:__subpackages__",
    ],
)

cc_test(
    name = "builtin_ops_test",
    srcs = ["register_test.cc"],
    deps = [
        ":builtin_ops",
        "//tensorflow/lite:mutable_op_resolver",
        "//tensorflow/lite/c:common",
        "//tensorflow/lite/schema:schema_fbs",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "builtin_ops",
    srcs = ["register.cc"],
    hdrs = [
        "builtin_op_kernels.h",
        "register.h",
    ],
    compatible_with = get_compatible_with_portable(),
    visibility = [
        "//tensorflow/lite:__subpackages__",
    ] + builtin_ops_visibility_allowlist(),
    deps = [
        "//tensorflow/lite:mutable_op_resolver",
        "//tensorflow/lite:tflite_with_xnnpack_optional",
        "//tensorflow/lite/core:cc_api_stable",
        "//tensorflow/lite/core/c:common",
        "//tensorflow/lite/kernels:builtin_op_kernels",
        "//tensorflow/lite/schema:schema_fbs",
    ],
)

# For internal usage by shared libraries only.
cc_library(
    name = "builtin_ops_all_linked",
    srcs = ["register.cc"],
    hdrs = [
        "builtin_op_kernels.h",
        "register.h",
    ],
    copts = tflite_copts(),
    # Limit visibility to TFLite only.
    visibility = [
        "//tensorflow/lite:__subpackages__",
    ],
    deps = [
        "//tensorflow/lite:framework_stable",
        "//tensorflow/lite:tflite_with_xnnpack_optional",
        "//tensorflow/lite/core:cc_api_stable",
        "//tensorflow/lite/core/c:common",
        "//tensorflow/lite/kernels:builtin_op_kernels",
        "//tensorflow/lite/schema:schema_fbs",
    ],
    alwayslink = 1,
)

tflite_self_contained_libs_test_suite(name = "self_contained_libs_test_suite")
