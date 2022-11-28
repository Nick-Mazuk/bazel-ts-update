load("@aspect_rules_ts//ts:defs.bzl", "ts_project")
load("@aspect_rules_js//js:defs.bzl", "js_test")
load("@aspect_rules_swc//swc:defs.bzl", "swc_transpiler")

ts_project(
    name = "lib",
    srcs = ["test.ts"],
    transpiler = swc_transpiler,
    declaration = True,
)

js_test(
    name = "test",
    data = [
        ":lib",
    ],
    entry_point = "test.js",
)
