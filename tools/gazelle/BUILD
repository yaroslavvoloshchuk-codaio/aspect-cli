load("@aspect_gazelle_prebuilt//:def.bzl", "aspect_gazelle")

# Self-host target for the `aspect gazelle` task.
#
# `languages = ["proto"]` is intentional and not a no-op pretense:
# aspect-cli has no .proto files in the workspace, so the proto language
# is a true no-op generator — it walks the tree but finds nothing to
# emit. We do NOT want the default language subset because it includes
# `starlark` (rewrites bzl_library targets for every .bzl file) and
# `visibility_extension` (rewrites visibility lists) — both would
# produce repo-wide BUILD-file churn that this PR is not the place to
# audit and accept.
#
# When/if the repo adopts a gazelle-managed language for real, swap
# `["proto"]` for the appropriate set (e.g. `["go", "proto"]` if we ever
# add real Go code, or `DEFAULT_LANGUAGES` for the standard subset).
aspect_gazelle(
    name = "gazelle",
    languages = ["proto"],
)
