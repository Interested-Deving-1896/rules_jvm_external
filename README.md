[update-readmes]   Mode: rewrite — migrating to template structure...
# rules_jvm_external

[![Built with Ona](https://ona.com/build-with-ona.svg)](https://app.ona.com/#https://github.com/Interested-Deving-1896/rules_jvm_external)

<!-- AI:start:what-it-does -->
_Description pending._
<!-- AI:end:what-it-does -->

## Architecture

<!-- AI:start:architecture -->
_Architecture documentation pending._
<!-- AI:end:architecture -->

## Install

<!-- Add installation instructions here. This section is yours — the AI will not modify it. -->

```bash
git clone https://github.com/Interested-Deving-1896/rules_jvm_external.git
cd rules_jvm_external
```

## Usage


See [bzlmod.md](./docs/bzlmod.md) for complete usage instructions.

```starlark
# MODULE.bazel

bazel_dep(name = "rules_jvm_external", version = "7.0.0")

maven = use_extension("@rules_jvm_external//:extensions.bzl", "maven")

maven.install(
    artifacts = [
        "junit:junit:4.12",
        "androidx.test.espresso:espresso-core:3.1.1",
        "org.hamcrest:hamcrest-library:1.3",
    ],
    repositories = [
        # Private repositories are supported through HTTP Basic auth
        "http://username:password@localhost:8081/artifactory/my-repository",
        "https://maven.google.com",
        "https://repo1.maven.org/maven2",
    ],
    lock_file = "//:maven_install.json",
)
```

Credentials for private repositories can also be specified using a property file
or environment variables. See the [Coursier
documentation](https://get-coursier.io/docs/other-credentials.html#property-file)
for more information. You may also use a `.netrc` file.

### Pinning and lock files

In order to support repeatable builds, and to avoid projects needing to perform
their own dependency resolution at build time, it is strongly recommend that
projects "pin" their dependencies. This is a three step process:

1. Add a `lock_file` attribute to the `install` tag. The lock file is traditionally
   called `maven_install.json`.
2. `touch maven_install.json BUILD.bazel` The lock file must exist before pinning
   but may be empty. It must also be a valid target. This command creates both of
   the required files.
3. `REPIN=1 bazel run @maven//:pin` This will generate the lock file.

You may now add the build and lock file to source control.

Subsequent repins are required every time you modify the artifacts or BOMs in
used in the dependency resolution. `rules_jvm_external` will fail the build and
notify you if a repin is ever required.

Next, reference the artifacts in the BUILD file with their versionless label:

```python
java_library(
    name = "java_test_deps",
    exports = [
        "@maven//:junit_junit",
        "@maven//:org_hamcrest_hamcrest_library",
    ],
)

android_library(
    name = "android_test_deps",
    exports = [
        "@maven//:junit_junit",
        "@maven//:androidx_test_espresso_espresso_core",
    ],
)
```

The default label syntax for an artifact `foo.bar:baz-qux:1.2.3` is `@maven//:foo_bar_baz_qux`. That is,

* All non-alphanumeric characters are substituted with underscores.
* Only the group and artifact IDs are required.
* The target is located in the `@maven` top level package (`@maven//`).

## Configuration

<!-- Document configuration options here. This section is yours — the AI will not modify it. -->

## CI

<!-- AI:start:ci -->
_CI documentation pending._
<!-- AI:end:ci -->

## Mirror chain

<!-- AI:start:mirror-chain -->
This repo is maintained in [`Interested-Deving-1896/rules_jvm_external`](https://github.com/Interested-Deving-1896/rules_jvm_external) and mirrored through:

```
Interested-Deving-1896/rules_jvm_external  ──►  OpenOS-Project-OSP/rules_jvm_external  ──►  OpenOS-Project-Ecosystem-OOC/rules_jvm_external
```

Changes flow downstream automatically via the hourly mirror chain in
[`fork-sync-all`](https://github.com/Interested-Deving-1896/fork-sync-all).
Direct commits to OSP or OOC are detected and opened as PRs back to `Interested-Deving-1896`.
<!-- AI:end:mirror-chain -->

## Contributors

<!-- AI:start:contributors -->
_Contributors pending._
<!-- AI:end:contributors -->

## Origins

<!-- AI:start:origins -->
_Original project — no upstream fork._
<!-- AI:end:origins -->

## Resources

<!-- AI:start:resources -->
_No additional resource files found._
<!-- AI:end:resources -->

## License

<!-- AI:start:license -->
[Apache-2.0](https://github.com/Interested-Deving-1896/rules_jvm_external/blob/master/LICENSE) © 2026 [Interested-Deving-1896](https://github.com/Interested-Deving-1896)
<!-- AI:end:license -->
