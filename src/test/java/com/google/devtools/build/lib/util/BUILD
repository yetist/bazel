load("@rules_java//java:defs.bzl", "java_library", "java_test")

package(
    default_testonly = 1,
    default_visibility = ["//src:__subpackages__"],
)

filegroup(
    name = "srcs",
    testonly = 0,
    srcs = glob(["*"]) + [
        "//src/test/java/com/google/devtools/build/lib/util/io:srcs",
        "//src/test/java/com/google/devtools/build/lib/util/subjects:srcs",
    ],
    visibility = ["//src:__subpackages__"],
)

java_test(
    name = "UtilTests",
    size = "small",
    srcs = glob(
        [
            "*.java",
        ],
        exclude = [
            "DependencySetWindowsTest.java",
            "ResourceFileLoaderTest.java",
        ],
    ),
    tags = [
        "foundations",
        "no_windows",
    ],
    test_class = "com.google.devtools.build.lib.AllTests",
    runtime_deps = [
        "//src/test/java/com/google/devtools/build/lib:test_runner",
    ],
    deps = [
        "//src/main/java/com/google/devtools/build/lib:build",
        "//src/main/java/com/google/devtools/build/lib:command-utils",
        "//src/main/java/com/google/devtools/build/lib:exitcode-external",
        "//src/main/java/com/google/devtools/build/lib:failure_detail_util",
        "//src/main/java/com/google/devtools/build/lib:filetype",
        "//src/main/java/com/google/devtools/build/lib:os_util",
        "//src/main/java/com/google/devtools/build/lib:resource-converter",
        "//src/main/java/com/google/devtools/build/lib:shell_escaper",
        "//src/main/java/com/google/devtools/build/lib:simple-log-handler",
        "//src/main/java/com/google/devtools/build/lib:single-line-formatter",
        "//src/main/java/com/google/devtools/build/lib:string_util",
        "//src/main/java/com/google/devtools/build/lib/actions:localhost_capacity",
        "//src/main/java/com/google/devtools/build/lib/analysis/platform",
        "//src/main/java/com/google/devtools/build/lib/clock",
        "//src/main/java/com/google/devtools/build/lib/cmdline",
        "//src/main/java/com/google/devtools/build/lib/shell",
        "//src/main/java/com/google/devtools/build/lib/skyframe/serialization/testutils",
        "//src/main/java/com/google/devtools/build/lib/vfs:pathfragment",
        "//src/main/java/com/google/devtools/build/lib/vfs/inmemoryfs",
        "//src/main/protobuf:failure_details_java_proto",
        "//src/test/java/com/google/devtools/build/lib/testutil",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:junit4",
        "//third_party:mockito",
        "//third_party:truth",
        "//third_party/protobuf:protobuf_java",
    ],
)

java_test(
    name = "ResourceFileLoaderTest",
    srcs = ["ResourceFileLoaderTest.java"],
    resources = ["ResourceFileLoaderTest.message"],
    deps = [
        "//src/main/java/com/google/devtools/build/lib:util",
        "//third_party:junit4",
        "//third_party:truth",
    ],
)

# Tests windows specific path handling on Unix.
java_library(
    name = "UtilWindowsTests_lib",
    srcs = ["DependencySetWindowsTest.java"],
    resources = ["ResourceFileLoaderTest.message"],
    deps = [
        "//src/main/java/com/google/devtools/build/lib:util",
        "//src/main/java/com/google/devtools/build/lib/vfs",
        "//src/main/java/com/google/devtools/build/lib/windows",
        "//src/test/java/com/google/devtools/build/lib/testutil",
        "//third_party:guava",
        "//third_party:junit4",
        "//third_party:truth",
    ],
)

java_test(
    name = "UtilWindowsTests",
    size = "small",
    jvm_flags = [
        "-Dblaze.os=Windows",
        "-Dbazel.windows_unix_root=C:/fake/msys",
    ],
    test_class = "com.google.devtools.build.lib.AllTests",
    runtime_deps = [
        ":UtilWindowsTests_lib",
        "//src/test/java/com/google/devtools/build/lib:test_runner",
    ],
)

test_suite(
    name = "windows_tests",
    tags = [
        "-no_windows",
        "-slow",
    ],
)

test_suite(
    name = "all_windows_tests",
    tests = [
        ":windows_tests",
        "//src/test/java/com/google/devtools/build/lib/util/io:all_windows_tests",
    ],
)
