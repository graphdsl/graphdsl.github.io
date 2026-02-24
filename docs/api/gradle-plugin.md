# Gradle Plugin

Plugin ID: `io.github.graphdsl.graphdsl-plugin`

## Applying the plugin

```kotlin title="build.gradle.kts"
plugins {
    id("io.github.graphdsl.graphdsl-plugin") version "0.1.0"
}
```

## Tasks

### `generateDsl`

Reads all `.graphqls` files from `schemaDir` and generates the Kotlin DSL sources into `build/generated/graphdsl/`.

```bash
./gradlew generateDsl
```

This task runs automatically before `compileKotlin`, so a normal build will always keep generated sources up to date.

## Extension reference

```kotlin
graphDsl {
    // Package for generated classes
    packageName.set("com.example.api.dsl")

    // Directory containing .graphqls files
    schemaDir.set("src/main/graphql")
}
```

See [Configuration](../configuration.md) for full option details.
