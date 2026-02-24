# Getting Started

## Requirements

- JDK 11+
- Gradle 8+
- A GraphQL schema file (`.graphqls`)

---

## 1. Apply the Gradle plugin

In your `build.gradle.kts`:

```kotlin
plugins {
    kotlin("jvm") version "2.0.0"
    id("io.github.graphdsl.graphdsl-plugin") version "0.1.0"
}
```

---

## 2. Add your schema

Place your `.graphqls` files in `src/main/graphql/`. For example:

```graphql title="src/main/graphql/schema.graphqls"
type Query {
    greeting: String
    author(id: ID!): Author
    post(id: ID!): Post
    authors: [Author!]!
    searchPosts(filter: PostFilterInput!): [Post!]!
}

type Mutation {
    createPost(input: CreatePostInput!): Post
    deletePost(id: ID!): Boolean
}

type Author {
    id: ID!
    name: String!
    email: String!
}

type Post {
    id: ID!
    title: String!
    content: String!
    author: Author!
    published: Boolean!
}

input PostFilterInput {
    authorId: ID
    titleContains: String
    published: Boolean
}

input CreatePostInput {
    title: String!
    content: String!
    authorId: ID!
}
```

---

## 3. Configure the plugin

```kotlin title="build.gradle.kts"
graphDsl {
    packageName.set("com.example.api.dsl") // package for generated files
    schemaDir.set("src/main/graphql")       // default, can be omitted
}
```

---

## 4. Generate the DSL

```bash
./gradlew generateDsl
```

Generated Kotlin sources are placed in `build/generated/graphdsl/` and automatically added to your compile classpath.

---

## 5. Use the generated DSL

```kotlin
import com.example.api.dsl.*

// Query
val getPost = query(name = "GetPost") {
    post(id = "42") {
        id
        title
        content
        author {
            name
            email
        }
    }
}

// Query with input
val search = query(name = "SearchPosts") {
    searchPosts(filter = PostFilterInput(published = true)) {
        id
        title
        author {
            name
        }
    }
}

// Mutation
val create = mutation(name = "CreatePost") {
    createPost(input = CreatePostInput(
        title = "Hello GraphDSL",
        content = "Type-safe queries are great.",
        authorId = "1"
    )) {
        id
        title
    }
}
```

!!! tip
    The generated DSL mirrors your schema exactly. If a field doesn't exist in the schema, it won't compile — catching errors at build time rather than runtime.

---

## Next steps

- [Configuration reference](configuration.md) — all plugin options
- [Gradle plugin API](api/gradle-plugin.md) — tasks and extension details
