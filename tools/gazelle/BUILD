load("@aspect_gazelle_prebuilt//:def.bzl", "aspect_gazelle")
load("@gazelle//:def.bzl", "gazelle", "gazelle_binary")

# Default gazelle target — uses aspect_gazelle_prebuilt so users don't
# need a Go toolchain. This is the recommended setup for most repos
# and the default `--gazelle-target` value of the `aspect gazelle` task.
#
# `languages = ["proto"]` is intentional: aspect-cli has no .proto
# files, so the proto language is a true no-op generator — it walks
# the tree but finds nothing to emit. We avoid the default language
# subset because it includes `starlark` (rewrites bzl_library targets
# for every .bzl file) and `visibility_extension` (rewrites visibility
# lists) — both would produce repo-wide BUILD-file churn we don't want
# implicit.
aspect_gazelle(
    name = "gazelle",
    languages = ["proto"],
)

# Build-from-source regression target. Some users prefer building
# gazelle from source via `bazel_dep(name = "gazelle")` + `rules_go`
# rather than pulling in a prebuilt binary — this target exercises
# that path so we catch breakage in the upstream gazelle macro / its
# wrapper / its flag handling. CI runs `aspect gazelle` against this
# target as a parallel job; the binary itself is a separately-compiled
# Go program with the proto language extension linked in.
gazelle_binary(
    name = "gazelle_from_source_binary",
    languages = [
        "@gazelle//language/proto",
    ],
)

gazelle(
    name = "gazelle_from_source",
    gazelle = ":gazelle_from_source_binary",
)
