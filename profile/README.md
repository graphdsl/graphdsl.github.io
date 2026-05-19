# GraphDSL

**Type-safe GraphQL Kotlin DSL code generator**

GraphDSL reads your GraphQL schema and generates a type-safe Kotlin DSL so you can build queries and mutations programmatically — no string templates, no typos, no guessing field names.

```kotlin
val query = query("GetPost") {
    post(id = "42") {
        id
        title
        author {
            name
            emailso th
        }
    }
}
// → query GetPost { post(id: "42") { id title author { name email } } }
```

---

## Projects

| Repository | Description |
|---|---|
| [graphql-kotlin-dsl](https://github.com/graphdsl/graphql-kotlin-dsl) | Core library, Gradle plugin, and CLI |
| [graphdsl.github.io](https://github.com/graphdsl/graphdsl.github.io) | Documentation site |

---

## Built with

**Language & Runtime**
- [Kotlin](https://kotlinlang.org/) 1.9 — JVM target 17
- [graphql-java](https://www.graphql-java.com/) — GraphQL schema parsing
- [kotlinx-metadata-jvm](https://github.com/JetBrains/kotlin/tree/master/libraries/kotlinx-metadata/jvm) — Kotlin type metadata inspection

**Code Generation**
- [StringTemplate 4](https://www.stringtemplate.org/) (ANTLR ST4) — template-driven source file generation
- [Javassist](https://www.javassist.org/) — bytecode utilities

**Tooling**
- [Gradle](https://gradle.org/) — build system with convention plugins and included builds
- [Clikt](https://ajalt.github.io/clikt/) — Kotlin CLI framework
- [JUnit 5](https://junit.org/junit5/) — testing

---

## Links

- [Documentation](https://graphdsl.github.io)
- [Getting started](https://graphdsl.github.io/getting-started)
- [Gradle plugin reference](https://graphdsl.github.io/api/gradle-plugin)
