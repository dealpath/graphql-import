# graphql-import [![Build Status](https://travis-ci.org/graphcool/graphql-import.svg?branch=master)](https://travis-ci.org/graphcool/graphql-import) [![npm version](https://badge.fury.io/js/graphql-import.svg)](https://badge.fury.io/js/graphql-import) [![Greenkeeper badge](https://badges.greenkeeper.io/graphcool/graphql-import.svg)](https://greenkeeper.io/)

Import &amp; export definitions in GraphQL SDL (also refered to as GraphQL modules)

## Install

```sh
yarn add graphql-import
```

## Usage

```ts
import { importSchema } from 'graphql-import'
import { makeExecutableSchema } from 'graphql-tools'

const typeDefs = importSchema('schema.graphql')
const resolvers = {}

const schema = makeExecutableSchema({ typeDefs, resolvers })
```

## Example

Assume the following directory structure:

```
.
├── a.graphql
├── b.graphql
└── c.graphql
```

`a.graphql`

```graphql
# import B from "b.graphql"

type A {
  # test 1
  first: String @first
  second: Float
  b: B
}
```

`b.graphql`

```graphql
# import C from 'c.graphql'

type B {
  c: C
  hello: String!
}
```

`c.graphql`

```graphql
type C {
  id: ID!
}
```

Running `console.log(importSchema('a.graphql'))` procudes the following output:

```graphql
type A {
  first: String @first
  second: Float
  b: B
}

type B {
  c: C
  hello: String!
}

type C {
  id: ID!
}
```

Please refer to [`src/index.test.ts`](src/index.test.ts) for more examples.

## Related topics & next steps

- Static import step as build time
- Namespaces
- Support importing from HTTP endpoints (or [Links](https://github.com/apollographql/apollo-link))
- Create RFC to add import syntax to GraphQL spec
