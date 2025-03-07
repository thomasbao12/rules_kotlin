# Copyright 2020 The Bazel Authors. All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
load("//kotlin/internal:toolchains.bzl", "kt_configure_toolchains")
load("//src/main/starlark/release:packager.bzl", "release_archive")
load("//src/main/starlark/core/repositories:versions.bzl", "versions")
load("@bazel_skylib//:bzl_library.bzl", "bzl_library")

# Configures the toolchains
kt_configure_toolchains()

release_archive(
    name = "pkg",
    srcs = glob(
        ["*.bzl"],
        exclude = ["opts.bzl"],
    ),
    src_map = {
        "BUILD.release.bazel": "BUILD.bazel",
        "opts.release.bzl": "opts.bzl",
    },
    deps = [
        "//kotlin/internal/js:pkg",
        "//kotlin/internal/jvm:pkg",
        "//kotlin/internal/lint:pkg",
        "//kotlin/internal/utils:pkg",
    ],
)

bzl_library(
    name = "internal",
    srcs = glob(["*.bzl"]),
    visibility = ["//kotlin:__subpackages__"],
    deps = [
        "//kotlin/internal/js",
        "//kotlin/internal/jvm",
        "//kotlin/internal/lint",
        "//kotlin/internal/utils",
        "//src/main/starlark",
    ] + [
        "@%s//:starlark" % v
        for v in versions.CORE
    ],
)
