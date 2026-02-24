# Configuration

## Gradle plugin extension

Configure GraphDSL in your `build.gradle.kts` using the `graphDsl` block:

```kotlin
graphDsl {
    packageName.set("com.example.api.dsl")
    schemaDir.set("src/main/graphql")
}
```

### Options

| Option | Type | Default | Description |
|---|---|---|---|
| `packageName` | `String` | `graphdsl.api.dsl` | Package name for all generated Kotlin files |
| `schemaDir` | `String` | `src/main/graphql` | Directory containing `.graphqls` schema files |

---

## Generated output

By default, generated sources are placed in:

```
build/generated/graphdsl/
```

This directory is automatically added to the `main` source set, so generated classes are available on the compile classpath without any extra configuration.

---

## CLI options

If you use the standalone CLI instead of the Gradle plugin:

```bash
java -jar graphdsl-cli.jar \
    --schema_files path/to/schema.graphqls \
    --generated_directory build/generated/graphdsl \
    --pkg_for_generated_classes com.example.api.dsl \
    --output_archive build/graphdsl-generated.zip  # optional
```

| Flag | Required | Description |
|---|---|---|
| `--schema_files` | Yes | Comma-separated list of `.graphqls` files |
| `--generated_directory` | Yes | Output directory for generated Kotlin sources |
| `--pkg_for_generated_classes` | No | Package name (default: `graphdsl.api.dsl`) |
| `--output_archive` | No | If set, zips the output and deletes the directory |

---

## Multi-schema projects

You can point `schemaDir` at any directory. GraphDSL picks up all `.graphqls` files inside it recursively:

```
src/main/graphql/
├── queries.graphqls
├── mutations.graphqls
└── types/
    ├── user.graphqls
    └── post.graphqls
```

All files are merged before generation, so types defined across files are resolved correctly.
