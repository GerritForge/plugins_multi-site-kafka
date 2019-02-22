load("//tools/bzl:junit.bzl", "junit_tests")
load(
    "//tools/bzl:plugin.bzl",
    "PLUGIN_DEPS",
    "PLUGIN_TEST_DEPS",
    "gerrit_plugin",
)

gerrit_plugin(
    name = "multi-site-kafka",
    srcs = glob(["src/main/java/**/*.java"]),
    manifest_entries = [
        "Gerrit-PluginName: multi-site-kafka",
        "Gerrit-Module: com.googlesource.gerrit.plugins.multisite.kafka.KafkaModule",
        "Implementation-Title: multi-site with kafka plugin",
        "Implementation-URL: https://review.gerrithub.io/admin/repos/GerritForge/plugins_multi-site-kafka",
    ],
    resources = glob(["src/main/resources/**/*"]),
    deps = [
        "@kafka_client//jar",
        "@commons-lang3//jar",
    ],
)

junit_tests(
    name = "multi_site_kafka_tests",
    srcs = glob(["src/test/java/**/*.java"]),
    resources = glob(["src/test/resources/**/*"]),
    tags = [
        "local",
        "multi-site-kafka",
    ],
    deps = [
        ":multi-site-kafka__plugin_test_deps",
    ],
)

java_library(
    name = "multi-site-kafka__plugin_test_deps",
    testonly = 1,
    visibility = ["//visibility:public"],
    exports = PLUGIN_DEPS + PLUGIN_TEST_DEPS + [
        ":multi-site-kafka__plugin",
        "@mockito//jar",
        "@wiremock//jar",
        "@kafka_client//jar",
        "@testcontainers-kafka//jar",
    ],
)
