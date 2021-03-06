# Description:
#   AWS C++ SDK

package(default_visibility = ["//visibility:public"])

licenses(["notice"])  # Apache 2.0

exports_files(["LICENSE"])

load("@%ws%//third_party:common.bzl", "template_rule")

cc_library(
    name = "aws",
    srcs = select({
        "@%ws%//tensorflow:linux_x86_64": glob([
            "aws-cpp-sdk-core/source/platform/linux-shared/*.cpp",
        ]),
        "@%ws%//tensorflow:darwin": glob([
            "aws-cpp-sdk-core/source/platform/linux-shared/*.cpp",
        ]),
    }) + glob([
        "aws-cpp-sdk-core/source/*.cpp",
        "aws-cpp-sdk-core/source/auth/**/*.cpp",
        "aws-cpp-sdk-core/source/config/**/*.cpp",
        "aws-cpp-sdk-core/source/client/**/*.cpp",
        "aws-cpp-sdk-core/source/external/**/*.cpp",
        "aws-cpp-sdk-core/source/internal/**/*.cpp",
        "aws-cpp-sdk-core/source/http/*.cpp",
        "aws-cpp-sdk-core/source/http/curl/**/*.cpp",
        "aws-cpp-sdk-core/source/http/standard/**/*.cpp",
        "aws-cpp-sdk-core/source/utils/*.cpp",
        "aws-cpp-sdk-core/source/utils/base64/**/*.cpp",
        "aws-cpp-sdk-core/source/utils/json/**/*.cpp",
        "aws-cpp-sdk-core/source/utils/logging/**/*.cpp",
        "aws-cpp-sdk-core/source/utils/memory/**/*.cpp",
        "aws-cpp-sdk-core/source/utils/stream/**/*.cpp",
        "aws-cpp-sdk-core/source/utils/threading/**/*.cpp",
        "aws-cpp-sdk-core/source/utils/xml/**/*.cpp",
        "aws-cpp-sdk-core/source/utils/crypto/*.cpp",
        "aws-cpp-sdk-core/source/utils/crypto/factory/**/*.cpp",
        "aws-cpp-sdk-s3/source/**/*.cpp",
    ]),
    hdrs = [
        "aws-cpp-sdk-core/include/aws/core/SDKConfig.h",
    ],
    defines = select({
        "@%ws%//tensorflow:linux_x86_64": [
            "PLATFORM_LINUX",
            "ENABLE_CURL_CLIENT",
            "ENABLE_NO_ENCRYPTION",
        ],
        "@%ws%//tensorflow:darwin": [
            "PLATFORM_APPLE",
            "ENABLE_CURL_CLIENT",
            "ENABLE_NO_ENCRYPTION",
        ],
        "//conditions:default": [],
    }),
    includes = [
        "aws-cpp-sdk-core/include/",
        "aws-cpp-sdk-s3/include/",
    ],
    deps = [
        "@curl//:curl",
    ],
)

template_rule(
    name = "SDKConfig_h",
    src = "aws-cpp-sdk-core/include/aws/core/SDKConfig.h.in",
    out = "aws-cpp-sdk-core/include/aws/core/SDKConfig.h",
    substitutions = {
        "cmakedefine": "define",
    },
)
