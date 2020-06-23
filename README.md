# Common Questions

These questions and answers are taken from various online resources, such as [HowToGraphQL](https://www.howtographql.com/advanced/5-common-questions/), [StackOverflow](https://stackoverflow.com/questions/50684231/what-is-an-exclamation-point-in-graphql), and [RisingStack](https://blog.risingstack.com/graphql-overview-getting-started-with-graphql-and-nodejs/).

### Is GraphQL a Database Technology?

No. GraphQL is often confused with being a database technology. This is a misconception, GraphQL is a query language for APIs - not databases. In that sense it's database agnostic and can be used with any kind of database or even no database at all.

### Is GraphQL only for React / Javascript Developers?

No. GraphQL is an API technology so it can be used in any context where an API is required.

On the backend, a GraphQL server can be implemented in any programming language that can be used to build a web server. Next to Javascript, there are popular reference implementations for Ruby, Python, Scala, Java, Clojure, Go and .NET.

Since a GraphQL API is usually operated over HTTP, any client that can speak HTTP is able to query data from a GraphQL server.

### How does GraphQL handle errors?

A successful GraphQL query is supposed to return a JSON object with a root field called "data". If the request fails or partially fails (e.g. because the user requesting the data doesn't have the right access permissions), a second root field called `"errors"` is added to the response:

```json
{
  "data": { ... },
  "errors": [ ... ]
}
```

### What is an exclamation point in GraphQL?

That means that the field is non-nullable. By default, all types in GraphQL are nullable. When non-null is applied to the type of a field, it means that if the server resolves that field to null, the response will fail validation.

### Where is GraphQL useful?

GraphQL helps where your client needs a flexible response format to avoid extra queries and/or massive data transformation with the overhead of keeping them in sync.

Using a GraphQL server makes it very easy for a client side developer to change the response format without any change on the backend.

With GraphQL, you can describe the required data in a more natural way. It can speed up development, because in application structures like top-down rendering in React, the required data is more similar to your component structure.

### What is difference between Mutation and Query?

Technically any GraphQL query could be implemented to cause a data write. But there is a convention that any operations that cause writes should be sent explicitly via a mutation.

Besides the difference in the semantic, there is one important technical difference:

Query fields can be executed in parallel by the GraphQL engine while Mutation top-level fields MUST execute serially according to the spec.

### What is GraphQL schema?

Every GraphQL server has two core parts that determine how it works: a schema and resolve functions.

The schema is a model of the data that can be fetched through the GraphQL server. It defines what queries clients are allowed to make, what types of data can be fetched from the server, and what the relationships between these types are.

For example:

```graphql
type Author {
  id: Int
  name: String
  posts: [Post]
}
type Post {
  id: Int
  title: String
  text: String
  author: Author
}
type Query {
  getAuthor(id: Int): Author
  getPostsByTitle(titleContains: String): [Post]
}
schema {
  query: Query
}
```
