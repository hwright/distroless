package(default_visibility = ["//visibility:public"])

load("@io_bazel_rules_docker//docker:docker.bzl", "docker_build")
load("@runtimes_common//structure_tests:tests.bzl", "structure_test")
load("@package_bundle//file:packages.bzl", "packages")

[docker_build(
    name = "python27" if not mode else mode[1:],
    # Based on //cc so that C extensions work properly.
    base = "//cc" + mode,
    debs = [
        packages["zlib1g"],
        packages["python2.7-minimal"],
        packages["libpython2.7-minimal"],
        packages["libpython2.7-stdlib"],
    ],
    entrypoint = [
        "/usr/bin/python2.7",
    ],
    symlinks = {
        "/usr/bin/python": "/usr/bin/python2.7",
    },
) for mode in [
    "",
    ":debug",
]]

structure_test(
    name = "python27_test",
    config = "testdata/python27.yaml",
    image = ":python27",
)
