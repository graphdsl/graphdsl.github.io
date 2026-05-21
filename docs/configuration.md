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
