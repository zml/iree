# Copyright 2019 The IREE Authors
#
# Licensed under the Apache License v2.0 with LLVM Exceptions.
# See https://llvm.org/LICENSE.txt for license information.
# SPDX-License-Identifier: Apache-2.0 WITH LLVM-exception

# Workspace file for the IREE project.
# buildozer: disable=positional-args

workspace(name = "iree_core")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:utils.bzl", "maybe")

###############################################################################
# Skylib
http_archive(
    name = "bazel_skylib",
    sha256 = "51b5105a760b353773f904d2bbc5e664d0987fbaf22265164de65d43e910d8ac",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-skylib/releases/download/1.8.1/bazel-skylib-1.8.1.tar.gz",
        "https://github.com/bazelbuild/bazel-skylib/releases/download/1.8.1/bazel-skylib-1.8.1.tar.gz",
    ],
)

load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")

bazel_skylib_workspace()
###############################################################################

http_archive(
    name = "bazel_features",
    sha256 = "06a9691becc357c1e4af011b9fb3239097503ce00607d9eb6b11ea0fac304039",
    strip_prefix = "bazel_features-1.35.0",
    url = "https://github.com/bazel-contrib/bazel_features/releases/download/v1.35.0/bazel_features-v1.35.0.tar.gz",
)

load("@bazel_features//:deps.bzl", "bazel_features_deps")

bazel_features_deps()

http_archive(
    name = "rules_cc",
    sha256 = "88661aba2ad049ae0be36eca8222c1911a397c077776aba8efa42b737eaa3152",
    strip_prefix = "rules_cc-0.2.3",
    url = "https://github.com/bazelbuild/rules_cc/releases/download/0.2.3/rules_cc-0.2.3.tar.gz",
)

load("@rules_cc//cc:extensions.bzl", "compatibility_proxy_repo")

compatibility_proxy_repo()

###############################################################################
# llvm-project

new_local_repository(
    name = "llvm-raw",
    build_file_content = "# empty",
    path = "third_party/llvm-project",
)

load("@llvm-raw//utils/bazel:configure.bzl", "llvm_configure")

llvm_configure(
    name = "llvm-project",
    # Keep this in sync with the targets in iree_llvm.cmake.
    targets = [
        "AArch64",
        "ARM",
        "RISCV",
        "X86",
        "NVPTX",
        "AMDGPU",
        "WebAssembly",
    ],
)

###############################################################################

###############################################################################
# All other IREE submodule dependencies

load("//build_tools/bazel:workspace.bzl", "configure_iree_cuda_deps", "configure_iree_submodule_deps")

configure_iree_submodule_deps()

configure_iree_cuda_deps()

###############################################################################
maybe(
    http_archive,
    name = "llvm_zlib",
    build_file = "@llvm-raw//utils/bazel/third_party_build:zlib-ng.BUILD",
    sha256 = "e36bb346c00472a1f9ff2a0a4643e590a254be6379da7cddd9daeb9a7f296731",
    strip_prefix = "zlib-ng-2.0.7",
    urls = [
        "https://github.com/zlib-ng/zlib-ng/archive/refs/tags/2.0.7.zip",
    ],
)

###############################################################################
maybe(
    http_archive,
    name = "llvm_zstd",
    build_file = "@llvm-raw//utils/bazel/third_party_build:zstd.BUILD",
    sha256 = "7c42d56fac126929a6a85dbc73ff1db2411d04f104fae9bdea51305663a83fd0",
    strip_prefix = "zstd-1.5.2",
    urls = [
        "https://github.com/facebook/zstd/releases/download/v1.5.2/zstd-1.5.2.tar.gz",
    ],
)

###############################################################################
maybe(
    http_archive,
    name = "com_google_protobuf",
    sha256 = "3d32940e975c4ad9b8ba69640e78f5527075bae33ca2890275bf26b853c0962c",
    strip_prefix = "protobuf-29.1",
    urls = [
        "https://github.com/protocolbuffers/protobuf/releases/download/v29.1/protobuf-29.1.tar.gz",
    ],
)

http_archive(
    name = "build_bazel_apple_support",
    sha256 = "ee20cc5c0bab47065473c8033d462374dd38d172406ecc8de5c8f08487943f2f",
    url = "https://github.com/bazelbuild/apple_support/releases/download/1.23.1/apple_support.1.23.1.tar.gz",
)

load(
    "@build_bazel_apple_support//lib:repositories.bzl",
    "apple_support_dependencies",
)

apple_support_dependencies()

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

protobuf_deps()

# load("@rules_java//java:rules_java_deps.bzl", "rules_java_dependencies")

# rules_java_dependencies()

load("@rules_java//java:repositories.bzl", "rules_java_toolchains")

rules_java_toolchains()

load("@rules_python//python:repositories.bzl", "py_repositories")

py_repositories()

http_archive(
    name = "build_bazel_rules_apple",
    sha256 = "de1c8bb872da6b03d2abff659178d3abfda5cc8d8a6b646fdab96ab2d00c9fa7",
    url = "https://github.com/bazelbuild/rules_apple/releases/download/4.1.2/rules_apple.4.1.2.tar.gz",
)

load(
    "@build_bazel_rules_apple//apple:repositories.bzl",
    "apple_rules_dependencies",
)

apple_rules_dependencies()

load(
    "@build_bazel_rules_swift//swift:repositories.bzl",
    "swift_rules_dependencies",
)

swift_rules_dependencies()

load(
    "@build_bazel_rules_swift//swift:extras.bzl",
    "swift_rules_extra_dependencies",
)

swift_rules_extra_dependencies()

apple_support_dependencies()
