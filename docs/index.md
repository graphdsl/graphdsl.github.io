# GraphDSL

**Type-safe GraphQL Kotlin DSL code generator**

GraphDSL reads your GraphQL schema and generates a type-safe Kotlin DSL so you can build queries and mutations programmatically — no string templates, no typos, no guessing field names.

---

## What it generates

Given a GraphQL schema like this:

```graphql
type Query {
    post(id: ID!): Post
    authors: [Author!]!
}

type Post {
    id: ID!
    title: String!
    author: Author!
}

type Author {
    id: ID!
    name: String!
    email: String!
}
```

GraphDSL generates a Kotlin DSL that lets you write:

```kotlin
val query = query(name = "GetPost") {
    post(id = "42") {
        id
        title
        author {
            name
            email
        }
    }
}
```

No strings. No reflection at runtime. Full IDE autocomplete.

---

## How to use it

=== "Gradle Plugin (recommended)"

    ```kotlin title="build.gradle.kts"
    plugins {
        id("io.github.graphdsl.graphdsl-plugin") version "0.1.0"
    }

    graphDsl {
        packageName.set("com.example.api.dsl")
        schemaDir.set("src/main/graphql")
    }
    ```

    Run `./gradlew generateDsl` — generated sources land in `build/generated/graphdsl/`.

=== "CLI"

    ```bash
    java -jar graphdsl-cli.jar \
        --schema_files schema.graphqls \
        --generated_directory build/generated/graphdsl \
        --pkg_for_generated_classes com.example.api.dsl
    ```

---

## Modules

| Module | Purpose |
|---|---|
| `schema` | GraphQL schema parsing |
| `mapper` | Maps GraphQL types to Kotlin types |
| `codegen` | DSL source file generation |
| `cli` | Standalone CLI runner |
| `gradle-plugins` | Gradle build integration |
| `utils` | Shared utilities |

---

[Get started :octicons-arrow-right-16:](getting-started.md){ .md-button .md-button--primary }
[View on GitHub :octicons-mark-github-16:](https://github.com/graphdsl/graphql-kotlin-dsl){ .md-button }
