workspace(
    name = "workspace",
    managed_directories = {"@npm": ["node_modules"]},
)

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# http_archive(
#     name = "aspect_rules_ts",
#     sha256 = "555f408bf664e553eb148f22dc2da9e82177413bd08d2d19180340962cf3ff86",
#     strip_prefix = "rules_ts-1.0.0-rc7",
#     url = "https://github.com/aspect-build/rules_ts/archive/refs/tags/v1.0.0-rc7.tar.gz",
# )

http_archive(
    name = "aspect_rules_ts",
    sha256 = "8993bfa4e4cae08a2c95df070197a8f3a77f8f186da3031344275254f61e936b",
    strip_prefix = "rules_ts-1.0.0-rc8",
    url = "https://github.com/aspect-build/rules_ts/archive/refs/tags/v1.0.0-rc8.tar.gz",
)

http_archive(
    name = "aspect_rules_swc",
    sha256 = "ad8e15e7714637b09a2e14e8ed3794b4de00e1da29259f93828c5bc80debb36b",
    strip_prefix = "rules_swc-0.19.3",
    url = "https://github.com/aspect-build/rules_swc/archive/refs/tags/v0.19.3.tar.gz",
)

##################
# rules_ts setup #
##################
load("@aspect_rules_ts//ts:repositories.bzl", "rules_ts_dependencies", TS_VERSION = "LATEST_VERSION")

rules_ts_dependencies(ts_version = TS_VERSION)

# Fetch and register node, if you haven't already
load("@rules_nodejs//nodejs:repositories.bzl", "nodejs_register_toolchains")

NODE_VERSION = "18.7.0"

nodejs_register_toolchains(
    name = "node",
    node_version = NODE_VERSION,
)

###################
# rules_swc setup #
###################

# Fetches the rules_swc dependencies.
# If you want to have a different version of some dependency,
# you should fetch it *before* calling this.
# Alternatively, you can skip calling this function, so long as you've
# already fetched all the dependencies.
load("@aspect_rules_swc//swc:dependencies.bzl", "rules_swc_dependencies")

rules_swc_dependencies()

# Fetches a pre-built Rust-node binding from
# https://github.com/swc-project/swc/releases.
# If you'd rather compile it from source, you can use rules_rust, fetch the project,
# then register the toolchain yourself. (Note, this is not yet documented)
load("@aspect_rules_swc//swc:repositories.bzl", "swc_register_toolchains", SWC_VERSION = "LATEST_VERSION")

swc_register_toolchains(
    name = "swc",
    swc_version = SWC_VERSION,
)
