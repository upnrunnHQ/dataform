package(default_visibility = ["//visibility:public"])

load("//tools:ts_library.bzl", "ts_library")

ts_library(
    name = "cloudbuild-badge",
    srcs = glob(["**/*.ts"]),
    deps = [
        "@npm//@google-cloud/storage",
        "@npm//@types/node",
    ],
)

filegroup(
    name = "index.js",
    srcs = ["cloudbuild-badge"],
    output_group = "es5_sources",
)

load("//tools/gcloud:gcloud_function.bzl", "deploy_pubsub_nodejs_gcloud_function")

deploy_pubsub_nodejs_gcloud_function(
    name = "deploy",
    srcs = [
        ":index.js",
        ":package.json",
    ],
    function_name = "updateCloudBuildStatusBadge",
    project = "tada-analytics",
    topic_name = "cloud-builds",
)
